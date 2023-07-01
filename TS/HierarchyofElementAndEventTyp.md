**[📆 2023-07-01 TIL]**

<br/>

# 📍 TypeScript에서 Element 및 Event 타입 위계

## 1. Element 타입 위계

```js
EventTarget < -Node < -Element < -HTMLElement;
```

- 예시
  - **video Element 위계** : `EventTarget` <- `Node` <- `Element` <- `HTMLElement` <- HTMLMediaElement` <- HTMLVedioElement`
- 주의 :
  - `querySelector` 함수의 결과값은 `Element` 타입이다. -> `as HTMLElement`로 타입 표명을 해줘야 함!
  ```ts
  const element = document.querySelector(".container") as HTMLElement;
  ```
  - 이벤트가 걸려 있는 Element라면 이중 표명 (Double assertion)을 해줘야 한다.
  ```ts
  const toggleHandler = (event: Event) => {
    let element = event as any as HTMLElement;
  };
  ```

<br/>

## 2. Event 타입 위계

```js
Event < -UIEvent;
```

- UIEvent : 간단한 사용자 인터페이스 이벤트, Event를 상속한다.

- 예시
  - **마우스 이벤트 위계** : `Event` <- `UIEvent` <- `MouseEvent`
  - **인풋 이벤트 위계**: `Event` <- `UIEvent` <- `InputEvent`
- 주의: \* 이중 표명 : 해당 이벤트를 상세히 정의해야 할 때는 이중 표명을 사용한다.
  `ts
    const toggleHandler = (event: Event) => {
  let mouseEvent = event as MouseEvent;
}
    `

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

타입스크립트에서 Dom, Event를 다룰 때는 타입 표명에 주의해야 한다. Elemnt와 Event의 타입이 가지는 위계를 이해하고, 경우에 따라 이중 표명을 사용하며 타입을 명확히 기입해줘야 에러가 발생하지 않는다.
