---
name: encapsulation
description: Patterns for encapsulting data
---

# Skill: Encapsulation of Data in Kotlin Classes

## Purpose

Guidelines on restricting access 
and visibility of data in a Kotlin class. 

## When to Use

- When code smell Feature Envy exists
- Working with Kotlin classes
- Working with Kotlin enum
- Working with Koltin data classes

## Constraints

- All instance variables will be private
- No accessor methods (getters or setters)
- Relax the constraint only for data classes if necessary

## Procedures

### Situation: Algorithm needs access to instance data

This is the Feature Envy code smell. Put the parts of the 
algorithm that needs the data in the same class with the data.

### Situation: A database or user interface needs instance data

Use an Observer pattern (called Listeners in Microsoft world) 
or Visitor pattern to extract the information. This should only
be used when another Kotlin module requires that data.

### Situation: Data needs to be printed

Use a Collecting Parameter, and pass it to the class to have
the class render itself in String format.

## Examples

### Chance class with Encapsulation

```kotlin
// fraction never exposed or changed
class Chance(private val fraction: Double) {
    infix fun and(other: Chance) = Chance(this.fraction * other.fraction)
    operator fun not() = Chance(1 - fraction)
    infix fun or(other: Chance) = !(!this and !other)
}
```

### Chance from a Database

Use a data class as response to the query, then build the
class from that data:

```kotlin
// Access to data can be relaxed
data class ChanceDto(val fraction) {
    fun toChance() = Chance(fraction)
}
```

## Notes

Also useful is the technique of Churning where two objects of the
same type perform the algorithm like Chance example. Each object
can access the private data of the other class if they are both
the same type.
