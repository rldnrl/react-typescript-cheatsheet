---
sidebar_position: 1
---

# Props 정의하기

## Props를 정의한 예제.

다음은 React + TypeScript를 사용할 때 많이 사용되는 타입을 나열한 것입니다.

```tsx
type UserProps = {
  username: string;
  age: number;
  disabled: boolean;
  /** 
   * string 배열 타입입니다.
   */
  tags: string[];
  /**
   * String Literal을 Union Type으로 작성했습니다. `string` 타입도 좁히는 것이 좋습니다.
   */
  status: "waiting" | "success";
  /** 
   * property들을 정의하지 않는 한, 어떤 것이든 들어올 수 있습니다.
   * ⚠️ Not Recommended - 타입은 최대한 구체적으로 정의하는 게 좋기 때문입니다.
   */
  information: object;
  /** 
   * property들을 구체적으로 정의한 타입입니다.
   */
  information: {
    company: string;
    techstack: string[];
  };
  /** 
   * 객체의 배열입니다. (일반적으로는 Type Alias를 이용합니다.)
   */
  followers: {
    username: string;
    githubUrl: string;
  }[];
  /**
   * 맵핑된 타입을 이용해서 타입을 정의했습니다.
   * ⚠️ Not Recommend - 타입은 최대한 구체적으로 정의하는 게 좋기 때문입니다.
   */
  mappedType: {
    [key in string]: string
  }
  /**
   * 어떤 함수든 들어올 수 있습니다.
   * ⚠️ Not Recommend - 타입은 최대한 구체적으로 정의하는 게 좋기 때문입니다.
   * [TypeScript Function Type](https://www.typescriptlang.org/docs/handbook/2/functions.html#function)
   */
  doSomething: Function
  /** 
   * 인자도 없고, 반환값도 없는 함수의 타입입니다.
   */
  onClick: () => void;
  /** 
   * props이 있는 함수의 타입입니다.
   */
  onClick: (id: string) => void;
  /** 
   * React 내부에 정의되어있는 이벤트 타입을 사용합니다.
   */
  onClick: (React.MouseEvent<HTMLButtonElement>) => void;
  /** 
   * React 내부에 정의되어있는 이벤트 핸들러 타입을 사용합니다.
   */
  onClick: MouseEventHandler<HTMLButtonElement>
}
```

위와 같이 타입을 많이 작성합니다. `Not Recommended`의 이유는 타입은 최대한 구체적으로 작성하는 것이 중요하기 때문입니다. 그래야 Intellisense 기능도 유용하게 사용할 수 있죠.

위의 `UserProps`를 `/** */`로 주석을 작성했는데요, 이것은 `JSDoc`이라고 합니다. 만약에 여러분이 **Design System**이나 **Library**를 만든다면, `JSDoc`을 작성하는 것이 매우 중요합니다. 가장 베스트는 타입으로 어떤 역할을 하는지 말해주는 것이지만, 그게 쉽지 않을 때가 많으니까요. (대부분의 경우 다른 사람이 작성한 코드를 이해하는 건 어렵습니다.)
