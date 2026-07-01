---
name: equals-hash-code
description: Patterns for implementing equals and hashCode in Kotlin
---

# Skill: Equals and hashCode in Kotlin Classes

## Purpose

Standardize implementation of equals and hashCode in Kotlin classes.

## When to Use

- When a class needs to be compared for equality
- **DO NOT** implement equals unless a class's behavior requires it. 

## Constraints

- Hash code must be consistent with equals. If two objects are equal, 
  they must have the same hash code, especially if rounding is needed for equals.
- Equals cannot throw an exception. Test to ensure that null and other types
  are handled gracefully.
- Data classes have equals and hashCode implemented by default. Ensure hashCode
  only uses immutable data.

## Procedures

### Situation: Class needs equals

Create a two-method implementation for equals. In the first overriden equals method, check 
for reference equality, then check for type, then use the implicit
casting to invoke a private equals method that takes the class as parameter.
In the second method, check equality for all the fields.

### Situation: Equals has been implemented

Implement hashCode so that two equal objects have the same hash code. 
If rounding is needed for equals, then the same rounding must be 
applied to the hash code.

## Examples

### Chance class with Encapsulation

```kotlin
// Equality with Doubles where rounding errors exist
class Chance(private val fraction: Double) {
    // Required equals API
    override fun equals(other: Any?) =
        this === other || other is Chance && this.equals(other)
    // Private method does the real testing of fields
    private fun equals(other: Chance) = (this.fraction - other.fraction).absoluteValue < EPSILON
    override fun hashCode() = (fraction / EPSILON).roundToLong().hashCode()
}
```

### Data class with mutable data

```kotlin
// Point has mutable Y value
class Point(private val xValue: Double, private var yValue: Double) {
    // Required equals API
    override fun equals(other: Any?) =
        this === other || other is Point && this.equals(other)
    // Private method does the real testing of both fields
    private fun equals(other: Point) = 
        (this.xValue - other.xValue).absoluteValue < EPSILON &&
        (this.yValue - other.yValue).absoluteValue < EPSILON
    // Only hash immutable field
    override fun hashCode() = ((xValue / EPSILON).roundToLong().hashCode()
}
```

### Full equals testing

```kotlin
class ChanceTest {
    @Test fun equals() {
        assertEquals(Chance(0.1), Chance(0.1))
        assertNotEquals(Chance(0.1), Chance(0.2))
        // Ensure no exception on null
        assertNotEquals(Chance(0.1), null)
        // Ensure no exception on different object type
        assertNotEquals(Chance(0.1), "not a Chance")
    }
}
```
