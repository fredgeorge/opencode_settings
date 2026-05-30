---
name: variable-names
description: Patterns for naming variables in Kotlin
---

# Skill: Variable Names in Kotlin Classes

## Purpose

Patterns for naming variables and parameters in Kotlin classes.

## When to Use

- All Kotlin instance variables
- All Kotlin parameters
- All Kotlin constants (including statics)

## Constraints

The descriptions below refer to "variables", but the same rules apply to parameters and constants.

- Name a variable or parameter descriptively, indicating its purpose or the type of data it holds. Domain-specific terms are often helpful, but avoid unnecessary jargon.
- Keep names as short as possible while still being descriptive. For example, "userName" is better than "theNameOfTheUser". 
- Only abbreviate if the abbreviation is widely understood and does not reduce clarity. For example, "num" for "number" is generally acceptable, but "n" for "number" may not be.
- Some ackronyms are acceptable if they are widely recognized in the domain. For example, "URL" or "ID" may be acceptable, but "UID" for "user ID" may not be.
- Avoid using single-letter variable names except for loop indices (e.g., "i")
- Lambda variables should also be named if the block is more than one line.
- Only the innermost lambda parameter can be named "it", again subject to the "one line" rule.
- Boolean variables should start with "is", "has", "can", "should", or some other verb that implies a yes/no answer. For example, "isEmpty", "hasChildren", "canRead", "shouldRetry".
- Variables for collections should be named with a plural noun that describes the collection. For example, "users", "orders", "items". 
- Variables for maps should be named with a plural noun that describes the values.
- An alternative map name would be to name the variable with a noun that describes the key, and then use "By" as a suffix. For example, "userById" for a map of users keyed by their ID. Use only if clarity is needed, particularly if several maps have the same value type but different key types.
- Don't prefix a name with "a" or "an" to indicate it's a parameter. This adds no clarity and is not a common convention in Kotlin.
- If a parameter is manipulated to be a instance variable, use the same name for both. For example, value: Number parameter could be value: Double = value.toDouble()

## Examples

See the descriptions above for examples of method names.

## Notes

Similarly, class names should be descriptive and domain-specific, but also concise. For example, "User" is better than "TheUserOfTheSystem".
