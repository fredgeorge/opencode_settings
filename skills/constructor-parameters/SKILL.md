---
name: constructor-parameters
description: Patterns for constructor parameters in Kotlin
---

# Parameters in Kotlin

## Purpose

Guidelines on creating and using constructor parameters in Kotlin.

## When to Use

- When a class is created with initial parameters
- When a parameter needs to be validated before being used in the class
- When a parameter may be one of several types, such as subclasses of Number

## Constraints

- This skill applies to each parameter independently.

## Procedures

### Situation: Parameter needs validation

Implement validation in an init{} block in the class. This allows for throwing exceptions if the parameter is invalid, preventing the creation of an instance with invalid data.

### Situation: Parameter may be one of several types

Convert the parameter to a private property of the class in an init{} block. Validation can also
be done before or after, whichever is more compact and expressive. Use the same name
for the parameter and the property, as they are in different scopes. This allows for flexible construction of the class while maintaining a consistent internal representation of the data.

## Examples

### Validation onlu

```kotlin
// Approval date must be in the past
class Approval(private val when: LocalDateTime) {
    init {
        require(when.isBefore(LocalDateTime.now())) { "Approval time cannot be in the future" }
    }
}
```

### Morphing a parameter to a private property with validation

```kotlin
// Support creation with Int or Double, and validate
class Chance(fraction: Number) {
    private fraction: Double
    init {
        fraction = fraction.toDouble()
        require(fraction in 0.0..1.0) { "Fraction must be between 0 and 1, inclusive" }
    }
}
```

## Notes

Parameter names follow rules in **variable-names** skill.
