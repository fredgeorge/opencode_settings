---
name: extension-methods
description: Patterns for using extension methods in Kotlin
---

# Extension Methods in Kotlin

## Purpose

Guidelines on creating and using extension methods in Kotlin.


## When to Use

- When class construction is clumsy with long lines with few parameters
- When a class in a closed packageis missing a method that would be useful to have in this module
- When the target of a method is a collection of some type

## Constraints

- Extensions methods that require access to private data must be in the class or its companion object
- Extension methods on collections of a class should be in the companion object of that class
- Extension methods with a single parameter should be marked with infix for better readability
    - Infix is prohibited in companion objects except for extension methods

## Procedures

### Situation: Class in another package is missing a logical method

Implement an extension method for that class locally in the module needing it.
Remember that private data will not be accessible. So this technique 
is used often to interface with databases, user interfaces, or formal APIs.

### Situation: A method having two collections of the same type as parameters

Make one of the collections the target of an extension method, and the other collection a parameter. This is often used for algorithms that combine two collections of the same type, such as union, intersection, or difference.

### Situation: Using the constructor of a class is clumsy

Examine the use of the class constructor. Is the essential data (the parameters)
difficult to discern in the line of code? If so, Use one of the parameters as
the target of an extension method, and the other parameters as parameters of the 
method. The intent of the instance will be cleare.

## Examples

### Clarity of intent for construction

```kotlin
// support specifying quantities like 3.5.kilometers
class Distance private constructor(private val unit: DistanceUnit,private val amount: Double) {
    companion object {
        val Double.kilometers get() = Distance(DistanceUnit.KILOMETERS, this)
        val Double.miles get() = Distance(DistanceUnit.MILES, this)
    }
    enum class DistanceUnit { KILOMETERS, MILES }
}
```

### Operations on two sets of the same type

```kotlin
// Confirm that all the required traits of an entity exist
enum class Trait { STRONG, SMART, FAST, RICH }
fun List<Trait>.hasAll(requiredTraits: List<Trait>) = requiredTraits.all { it in this }
```

## Notes

This is another technique for _Encapsulation_ by placing extension methods in the
companion object of the class with the private data. Usage requires importing
the class's companion object.
