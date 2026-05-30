---
name: kotlin-refactor
description: Safe Kotlin refactoring patterns
---

# Kotlin Refactoring

## Purpose
Perform safe refactoring of Kotlin code while preserving behavior.

## When to Use
- Reducing method complexity
- Extracting reusable abstractions
- Improving readability
- Migrating imperative code to idiomatic Kotlin

## Constraints
- Preserve public APIs unless explicitly instructed
- Do not change test behavior
- Prefer immutable data structures
- Prefer expression-bodied functions when readable
- Avoid unnecessary abstraction

## Procedure
1. Read all related files before editing
2. Identify behavioral boundaries
3. Refactor incrementally
4. Update imports and formatting
5. Re-run tests mentally or explicitly
6. Summarize changes and risks

## Kotlin Preferences
- Prefer sealed interfaces over enums for extensibility
- Prefer data classes for immutable DTOs
- Exploit extension functions for clarity
- Use scope functions (let, also, apply) to reduce 
 temporary variables

## Example

### Before
kotlin fun isAdult(age: Int): Boolean {     if (age >= 18) {         return true     } else {         return false     } } 

### After
kotlin fun isAdult(age: Int) = age >= 18 

## Notes
Favor clarity over cleverness.
