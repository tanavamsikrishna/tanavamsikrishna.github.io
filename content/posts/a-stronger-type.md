---
draft: false
title: Type for non-obvious data types
date: 2020-03-22T17:49:09+0530
description: Type for non-obvious data types
tags: [programming]
---

## Preface
I am generally convinced of the merits of static typing. But usually, I find that the static typing of most modern languages is not strong enough. Sometimes, the type information provided by type is inconclusive or misleading. If I say the type of variable is `String`, what is the maximum information you got? That it is a bunch of characters. Of course, so, we use descriptive variables names. If it was a `name: String`? We will know that the bunch of characters represent the name of an entity/person etc.. But specifically, if I want to convey the property, that a function `getName()` returns the name of a person in a `<last-name>, <first-name>` format. Is it going to be `getLastNameFirstName(): String`? And then it can get complex based on your requirements. Usually a snippet of documentation is added to properly explain that the `getName()` function provides a name in `<last-name>, <first-name>` format.

1. Sometimes, we use global standards & metric systems. Like using `ISO 8601` format for date-times.
2. We can specify that an object is not null by using the `@NonNull` annotation.

All of the above techniques can come together to give the best possible description of the type. But they still do not provide a complete solution.

One way of accurately describing a type is by using a custom annotation which validates the properties of the type. (Similar to the usage of `@NonNull`). And it is the subject of this article.

## The Idea
- By having an annotation `TypeRequirement`:
```kotlin
@Retention(AnnotationRetention.SOURCE)
annotation class TypeRequirement(val value: KClass<out Consumer<in Any?>>)
```
The above annotation take a class of type `Consumer`.
- The logic of describing the type can be done inside a subclass of `Consumer` like so:
```kotlin
class LastNameFirstNameAssertion : Consumer<Any?> {
    override fun accept(t: Any?) {
        assertTrue { t is String }
        t as String
        val nameParts = t.split(",")
        assertTrue { nameParts.size == 2 }
        nameParts.forEach { assertTrue { it.isNotBlank() } }
    }
}
```
The above consumer just asserts that a `String` passed to it has 2 non blank sub-strings separated by a comma.

- And finally can be used like so:
```kotlin
@TypeRequirement(LastNameFirstNameAssertion::class)
fun getName(): String {
    return "Timberlake, Justin"
}
```

### Value addition
1. Developer now understands that the values returned by `getName()` function satisfy the assertions in the `LastNameFirstNameAssertion#accept()` method
2. The type assertions can be injected into the test cases. For example by mocking the `getName()` method, and:
    1. Instead substituting it with a call to the actual `getName()` method
    2. Then, validating the output using the annotation's value parameter's `accept()` method
    3. And eventually returning the value returned by the preceding call to `getName()` method

By placing the `LastNameFirstNameAssertion` in a different module and by using `@Retention(AnnotationRetention.SOURCE)` on `TypeRequirement`, all traces of this type checking can be removed from the produced class files and the project artefact (jar file)

## Closing comments
There is some support from system programming languages for such kinds type description. `c++20`'s `concepts` or the `rust` language's `where` clause. The above technique or something similar is not something JVM targeting compilers support out of the box (for doing the type validation during the compilation phase).

But, currently, Kotlin compiler does the automatic type inference inside an if statement checking for type of an object. i.e. the following is valid.
```kotlin
val a: Any = get_val()
if (a is String) {
    print(a.substring(0, 10))
}
```
Variable `a` got inferred as of type `String` and thus the subsequent call to `substring` inside the `if` block is compilable. This is one step forward. But, the above case of type inference is done as a very special case. As substituting `a is String` with `String::class.isInstance(a)` will not help the compiler to do the type inference.
