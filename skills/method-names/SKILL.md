---
name: method-names
description: Patterns for naming methods in Kotlin
---

# Skill: Method Names in Kotlin Classes

## Purpose

Patterns for naming methods in Kotlin classes. 

## When to Use

- All Kotlin instance methods
- All Kotlin extension methods
- All Kotlin companion object methods

## Constraints

- Methods that return a Boolean should start with "is", "has", "can", "should", or some other verb that implies a yes/no answer. For example, "isEmpty", "hasChildren", "canRead", "shouldRetry".
- Methods that return something other than a Boolean should be named with a noun that describes what is returned. For example, "total", "riskLevel", "userName".
- Methods that perform an action should be named with a verb that describes the action. For example
, "calculateTotal", "sendEmail", "updateStatus", "validateInput".
- Methods that return a collection should be named with a plural noun that describes the collection. For example, "users", "orders", "items". This includes maps.
- Avoid using "get" or "set" prefixes in method names, as prefix adds nothing to the clarity of the method's return value. For example, "getUserName" should be renamed to "userName", and "setUserName" should be renamed to "userName" with a parameter.
- A method should either do something, or return something, but not both. This may be appropriate at times, but explicitly note that for further review. Callers of such methods often assume there are no side effects, and this can lead to bugs.

## Procedures

### Situation: Algorithm needs access to instance data

For each method:

1. Determine if the method returns anything (a Boolean, a collection, or some other type)
2. If the method returns a Boolean, rename it to start with "is", "has", "can", "should", or some other verb that implies a yes/no answer about some state of the class.
3. If the method returns something other than a Boolean, rename it to a noun that describes what is returned.
4. If the method returns a collection, rename it to a plural noun that describes the collection.
5. If the method performs an action, rename it to a verb that describes the action.
6. If the method has side effects, explicitly note that for further review.

## Examples

See the descriptions above for examples of method names.

## Notes

Also useful is the technique of Churning where two objects of the
same type perform the algorithm like Chance example. Each object
can access the private data of the other class if they are both
the same type.
