# Generics and Typed Promises

## Introduction

Generics let us write reusable code while preserving the relationship between input and output types. Instead of building separate functions for strings, numbers, and objects, we introduce a type parameter such as `T`. The compiler substitutes the appropriate type when the function is used.

## Reusable Functions with `T`

Consider an identity function that returns exactly what it receives:

```typescript
function identity<T>(value: T): T {
  return value;
}

const count = identity<number>(42);
const label = identity("ready");
```

In the second call, TypeScript infers that `T` is `string`. The function remains reusable without sacrificing type checking.

## Generics with Asynchronous Results

A `Promise<T>` describes a future result of type `T`. It tells TypeScript what a successful asynchronous operation will return:

```typescript
interface Profile {
  id: number;
  username: string;
}

async function loadProfile(): Promise<Profile> {
  return { id: 1, username: "Fahad" };
}

async function showUsername(): Promise<string> {
  const profile = await loadProfile();
  return profile.username;
}
```

Because `loadProfile()` returns `Promise<Profile>`, the value obtained through `await` is typed as `Profile`. Trying to access a nonexistent property, such as `profile.age`, causes a compile-time error. Note that a TypeScript type does not validate untrusted API data at runtime; external responses still need validation.

## Conclusion

Generics are valuable for collections, utility functions, and APIs. Combined with `Promise<T>`, they make asynchronous code predictable, readable, and easier to maintain. They express the expected result without resorting to the unsafe `any` type.
