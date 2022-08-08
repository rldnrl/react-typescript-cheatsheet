---
sidebar_position: 2
---

# Type or Interface

`Props`나 객체 타입을 정의할 때, 여러분은 "`type`을 사용할까?", "`interface`를 사용할까?" 고민에 빠질 겁니다.

## 결론
Type이 필요할 때까지는 Interface를 사용하세요.

## Tip
- Library를 만들 때는 Third Party Library의 [Ambient 타입](https://isamatov.com/typescript-ambient-module/)을 작성할 때는 `interface`를 사용하세요. 여러분이 작성하다가 빠진 타입이 있거나 필요한 타입이 있을 수 있기 때문입니다. `interface`는 병합하여 확장할 수 있습니다.

- `Props`나 `State` 같은 경우는 `type`을 사용하세요. 확장할 필요가 없기 때문입니다.

특징을 요약하자면 다음과 같습니다.

## Type Alias은 확장에 닫혀 있고, Interface는 확장에 열려 있습니다.

### Type Alias

```tsx
type User = {
  firstName: string
  lastName: string
  age: number
}

// Error!!! Duplicate identifier 'User'
type User = {
  email: string
}
```

### Interface

```tsx
interface User {
  firstName: string
  lastName: string
  age: number
}

interface User {
  email: string
}
```

**결과**

```tsx
interface User = {
  firstName: string
  lastName: string
  age: number
  email: string
}
```

## Type Alias는 확장할 때 `&`를 사용합니다.

```tsx
type BirdType = {
  wings: number
}

type Owl = { nocturnal: true } & BirdType
type Robin = { nocturnal: false } & BirdInterface
```

## 둘 다 `extends`를 사용할 수 있습니다.

```tsx
type BirdInterface = {
  wings: number
}

interface Peacock extends BirdType {
  colorful: true
  flies: false
}

interface Chicken extends BirdInterface {
  colorful: false
  flies: false
}
```

## Type Alias를 통해 `implements`를 사용할 경우, Union 타입이 들어간 것은 사용할 수 없습니다.

```tsx
type Name = {
  firstName: string
  lastName: string
}

type UserInfo =
  | Name
  | {
      age: number
    }

// Error!!! A class can only implement an object type
// or intersection of object types with statically known members.
class User implements UserInfo {}
```

## Type Alias를 통해 `extends`를 사용할 경우, Union 타입이 들어간 것은 사용할 수 없습니다.

```tsx
type Name = {
  firstName: string
  lastName: string
}

type UserInfo =
  | Name
  | {
      age: number
    }

// Error!!! 'UserInfo' only refers to a type, but is being used as a value here.
class User extends UserInfo {}
```
