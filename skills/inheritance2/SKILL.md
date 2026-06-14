---
name: inheritance
description: Patterns for inheritance, subclasses, and use of protected
---

# Inheritance in Kotlin

## Purpose

Guidelines on creating and using inheritance, subclasses, and protected access in Kotlin.


## When to Use

- When two classes have a strong "is-a" relationship, and one class can be considered a specialized version of the other
- When you want to reuse code from a parent class in a child class, and the child class can override or extend the behavior of the parent class

## When Not to Use

- **DO NOT** use inheritance if the subclass doesn't need most of the methods of the superclass. This is a sign that the "is-a" relationship is not strong enough, and composition may be a better choice.
- **DO NOT** use inheritance if the subclass needs to override most of the methods of the superclass. This is a sign that the subclass is not really a specialized version of the superclass, and composition may be a better choice.

## Constraints

- Access to immutable superclass fields should be protected, not private, to allow subclasses to use them without exposing them to the outside world.
- Access to mutable superclass fields should only be readonly. The field should be marked private, and a protected getter should be provided for subclasses to access the field without allowing them to modify it directly.

## Procedures

### Situation: Two classes have much common code

If two classes have much common code, and one class can be considered a specialized version of the other, consider using inheritance. The common code can be placed in the superclass, and the specialized behavior can be implemented in the subclass.

If two classes have much common code, but no clear "is-a" relationship, consider extracting
the common code into a separate class, and have each class delegate to that class instead of using inheritance.

### Situation: A subclass needs to access a field from the superclass

If the field is immutable, mark it as protected in the superclass. This allows the subclass to access it directly without exposing it to the outside world.

If the field is mutable and the subclass needs to read it, mark it as private in the superclass and provide a protected getter for the subclass to access it. This allows the subclass to read the field without allowing it to modify it directly, preserving encapsulation.

## Examples

## Notes

This is another technique for _Encapsulation_ by placing constraining access to fields in the superclass to only subclasses that require access.
