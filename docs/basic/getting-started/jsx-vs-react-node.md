---
sidebar_position: 3
---

# JSX.Element vs ReactNode

## `JSX.Element`
`JSX.Element`는 `React.createElement`가 반환하는 타입입니다.

### `JSX.Element` 타입

```ts
declare global {
  namespace JSX {
    interface Element extends React.ReactElement<any, any> { };
  }
}  
```

### `createElement` 타입

```ts
// Custom components
function createElement<P extends {}>(
  type: FunctionComponent<P>,
  props?: Attributes & P | null,
  ...children: ReactNode[]): FunctionComponentElement<P>;
function createElement<P extends {}>(
  type: ClassType<P, ClassicComponent<P, ComponentState>, ClassicComponentClass<P>>,
  props?: ClassAttributes<ClassicComponent<P, ComponentState>> & P | null,
  ...children: ReactNode[]): CElement<P, ClassicComponent<P, ComponentState>>;
function createElement<P extends {}, T extends Component<P, ComponentState>, C extends ComponentClass<P>>(
  type: ClassType<P, T, C>,
  props?: ClassAttributes<T> & P | null,
  ...children: ReactNode[]): CElement<P, T>;
function createElement<P extends {}>(
  type: FunctionComponent<P> | ComponentClass<P> | string,
  props?: Attributes & P | null,
  ...children: ReactNode[]): ReactElement<P>;
```

다음과 같이 타입이 정의되어 있습니다. 반환 타입이 다른 것 같지만, 이것은 `React.Element`를 `extends`해서 사용하고 있기 때문에 결국에는 `JSX.Element`로 인터페이스가 맞춰지는 겁니다. 또한 컴포넌트를 만들게 되면 기본적으로 `JSX.Element`로 추론합니다.

## `ReactNode`
`ReactNode`는 컴포넌트가 반환할 수 있는 값의 집합입니다.

```ts
type ReactNode = ReactElement | string | number | ReactFragment | ReactPortal | boolean | null | undefined;
```

`ReactNode`는 `children` 타입으로 사용합니다.