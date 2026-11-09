# Type Narrowing in TypeScript

## Introduction

Type narrowing is the process of reducing a broad type to a more specific one after checking a value. This matters when a parameter can hold several kinds of data. A union type, such as `string | number`, is flexible, but you cannot safely call string methods until TypeScript knows the value is a string.

## Using `typeof`

The `typeof` operator checks primitive JavaScript types. Here, TypeScript permits `toUpperCase()` only inside the string branch:

```typescript
function describe(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}
```

## Using `instanceof`

For class instances, `instanceof` can identify the object's constructor. It is especially helpful with built-in types such as `Date`:

```typescript
function formatValue(value: Date | string): string {
  if (value instanceof Date) {
    return value.toISOString();
  }
  return value.trim();
}
```

## Using `in`

The `in` operator distinguishes objects based on available properties:

```typescript
type Cat = { meow: () => string };
type Dog = { bark: () => string };

function animalSound(animal: Cat | Dog): string {
  if ("meow" in animal) {
    return animal.meow();
  }
  return animal.bark();
}
```

## Conclusion

Type narrowing helps us handle unions without unsafe type assertions. By using ordinary runtime checks, TypeScript can verify which operations are valid in each branch. This leads to clearer code and catches mistakes during development rather than after deployment.
