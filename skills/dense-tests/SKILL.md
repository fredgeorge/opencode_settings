---
name: dense-tests
description: Test code should be compact to ease readability and understanding
---

# Dense Tests

## Purpose

Tests represent how to use the functional code. They should be as compact as possible to make it easy to read and understand how the functional code is used. Dense tests are a style of writing tests that emphasizes compactness and readability.

## When to Use

- When there are many variations for tests of a single function
- When multiple aspects of a result need to be tested

## Procedure

1. If the construction of an item is short, inline the
   construction in the assert rather than create a variable for it.
1. If several valid values for an API are to be tested, 
   group them into one test method.
1. If general setup for a test is needed, and different variations
   of the test are needed, create a different test class for
   each variation.

## Examples

### Multiple And Tests for Chance class

**DON'T** DO THIS:
```kotlin
@Test fun `and with large values`() {
    val c1 = Chance(0.7)
    val c2 = Chance(0.8)
    assertEquals(Chance(0.56), c1 and c2)}
```

**DO THIS** INSTEAD
```kotlin
@Test fun and() {
    assertEquals(Chance(0.25), Chance(0.5) and Chance(0.5))
    assertEquals(Chance(0.56), Chance(0.8) and Chance(0.7))
    assertEquals(Chance(0.8), Chance(0.8) and Chance(1.0))
    assertEquals(Chance(0.7), Chance(1.0) and Chance(0.7))
    assertEquals(Chance(0.0), Chance(0.8) and Chance(00))
    assertEquals(Chance(0.0), Chance(0.0) and Chance(0.7))
}
```

### Multiple Aspects Tested

```kotlin
@Test fun trace() {
    Helper().trace().also { trace ->
        assertEquals(2, trace.errors.size)
        assertEquals("Helper", trace.errors[0])
        assertEquals("Calculation", trace.errors[1])
        assertEquals(FAILED, trace.result)
    }
}
```