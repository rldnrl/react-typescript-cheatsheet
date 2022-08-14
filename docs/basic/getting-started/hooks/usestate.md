---
sidebar_position: 1
---

# useState()

먼저 `useState`함수의 타입이 어떻게 정의되어 있는지 살펴봅시다.

```tsx
function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>];

function useState<S = undefined>(): [S | undefined, Dispatch<SetStateAction<S | undefined>>];
```

`initialValue`의 타입이 원시 타입인 경우 TypeScript가 추론하도록 하는 게 좋습니다.

```tsx
const [username, setUsername] = useState('') // username: string
const [age, setAge] = useState(0) // age: number
const [toggle, setToggle] = useState(false) // toggle: boolean
```

`initialValue`에 아무 것도 넣지 않는 경우 `undefined`로 추론됩니다. 따라서 `initialValue` 값을 채워주는 것이 좋습니다.

```tsx
const [username, setUsername] = useState() // username: undefined
```

특정 타입인 경우 제네릭을 활용하는 것이 좋습니다.

```tsx
type User = {
  username: string
  age: number
}

const [user, setUser] = useState<User>({
  username: '',
  age: 0
})

type Users = User[]

const [users, setUsers] = useState<Users>([])
```

특정 타입을 제네릭으로 넣어줬지만, `initialValue`에 값을 넣지 않을 경우, 그 타입에 `undefined`로 정의됩니다.

```tsx
type User = {
  username: string
  age: number
}

const [user, setUser] = useState<User>() // user: User | undefined

type Users = User[]

const [users, setUsers] = useState<Users>() // users: Users | undefined
```
