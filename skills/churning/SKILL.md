---
name: churning
description: Algorithms style with multiple instances of the same class
---

# Churning

## Purpose

Strongly prefer algorithms that have two or more objects 
of the same type interact to create the result.

## When to Use

- When it seems a getter in needed
- Keeping a class strongly encapsulated
- Making sure an algorithm isn't duplicated elsewhere

## Procedure

1. Identify portions of the algorithm that require
 the same field from two or more instances of a class
1. Extract that part of the algorithm into a 
 separate method in the class with the field
1. Invoke that extracted method to get the
 desired result

## Examples

### Chance class using Churning

```kotlin
// Algorithms kept strickly within class
class Chance(private val fraction: Double) {
    infix fun and(other: Chance) = 
        Chance(this.fraction * other.fraction)
    operator fun not() = Chance(1 - fraction)
    infix fun or(other: Chance) = !(!this and !other)
}
```