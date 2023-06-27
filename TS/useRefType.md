**[📆 2023-06-27 TIL]**

<br/>

# 📍 useRef + Typescript

- typescript에서 useRef hook이 담고 있는 current의 type을 어떻게 지정해야 할지 몰라 어려움을 겪은 적이 있었다.(
  _Type 'MutableRefObject<... | undefined>' is not assignable to type .._ 와 같은 에러를 마주친 적이 많다.)
  따라서 useRef의 type 지정에 대해 정리해보고자 한다.

### useRef?

- current 프로퍼티에 변경 가능한 값을 담고 있는 '상자'
- React Hook의 일종으로, 인자로 넘어온 초깃값을 useRef 객체의 `current` 프로퍼티에 저장한다.
- DOM 객체를 직접 가리켜 내부 값을 변경하거나, 변경되어도 컴포넌트가 리렌더링 되지 않도록 하기 위한 값들을 저장할 때 주로 사용된다.
- useRef의 반환 타입인 `MutaleRefObject`와 `RefObject`의 정의

```ts
interface MutableRefObject<T> {
  current: T;
}

interface RefObject<T> {
  readonly current: T | null;
}
```

<br/>

### useRef의 3가지 정의

- [@types/react의 index.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react/index.d.ts#L1021-L1065)를 보면 useRef는 3개의 정의가 오버로딩 되어 있다.

#### 1. 제네릭 타입이 인자의 타입과 동일한 경우(<T>로 일치)

- `useRef<T>(initialValue: T): MutableRefObject<T>;`
- **current 프로퍼티 그 자체를 직접 변경 가능하다.**

```ts
const localVarRef = useRef<number>(0);

const handleButtonClick = () => {
  if (localVarRef.current) {
    localVarRef.current += 1;
    console.log(localVarRef.current); // 1 => 즉, current 그 자체를 변경 가능하다.
  }
};
```

#### 2. 인자의 타입이 null이 허용될 경우

- `useRef<T>(initialValue: T|null): RefObject<T>;`
- RefObject<T>를 반환한다. 즉, current 프로퍼티를 직접 수정할 수 없다.

* 그러나 current 자체만 읽기 전용이기 때문에, current의 하위 프로퍼티인 **`value`**와 같은 값은 수정이 가능하다. (읽기 전용이 얕다)

```ts
const localVarRef = useRef<number>(null);

const handleButtonClick = () => {
  if (localVarRef.current) {
    localVarRef.current += 1; // 에러 발생! -> (current 값을 변경할 수 없으므로!)
    console.log(localVarRef.current);
  }
};
```

#### 3. 제네릭 타입이 undefined인(제공하지 않은) 경우

- `useRef<T = undefined>(): MutableRefObject<T | undefinede>`
- MutableRefObject를 반환하지만 타입이 다르다.

```ts
 const inputRef = useRef<HTMLInputElement>();

 ...

 <input ref={inputRef} /> // 에러 발생! -> (컴포넌트 참조 시에는 MutableRefObject가 아닌 RefObject를 넣어야하므로)
```

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

useRef hook은 3가지 정의가 있고, 정의에 따라 반환되는 type 값이 다르다.
그러므로, **(1) 로컬 변수 용도로 useRef를 사용하는 것이라면 `MutableRefObject`를 사용해야 하므로 1번 케이스와 같이 제네릭 타입과 같은 타입의 초깃값을 넣어줘야 한다. (2) 또한, DOM을 직접 조작하기 위한 current 프로퍼티로 userRef 객체를 사용할 경우, 2번 케이스와 같이 `RefObject<T>`를 사용해야 하므로 초깃값으로 null을 넣어줘야 한다.**

(1) 로컬 변수 용도로 useRef 사용하는 경우

```ts
const localRef = useRef<number>(0);
```

(2) DOM을 직접 조작하기 위해 프로퍼티로 useRef 객체를 사용할 경우

```ts
const inputRef = useRef<HTMLInputElement>(null);
```
