**[📆 2023-06-23 TIL]**

<br/>

# 📍 React에서 Props Drilling을 해결하는 전략들은 무엇이 있을까?

### ✔️ Props Drilling이란?

단방향 데이터 흐름이라는 리액트의 특성 상, props를 전달하기 위해서 하위 컴포넌트를 거쳐야 한다. 이때 props를 오로지 하위 컴포넌트로 전달하는 용도로만 쓰이는 컴포넌트를 거치며 데이터를 전달하는 과정이 발생하기도 하는데, 이러한 현상을 `props Drilling` 이라 한다.

- **Props Drilling의 장점**

  - 컴포넌트 간에 데이터를 전달하는 가장 쉽고 빠르게 전달 할 수 있다.
  - **작은 프로젝트**에서는 전역 상태관리보다 값이 어디서 사용되는지 더 명시적이며, 값을 추적하는데 더 쉽고, 코드 변경이 애플리케이션의 다른 영역에 어떤 영향을 주는지 파악하는데 용이하다.

- **Props Drilling의 단점**

  - 프로젝트의 규모가 커지고 공유해야 하는 state가 늘어나면 props drilling으로 코드가 매우 복잡해지고 비효율적인 상황이 발생한다.
  - **여러 개의 컴포넌트를 타고 내려가다보면 이 props가 어디서부터 시작된건지 파악하기 쉽지 않아지고, 유지 보수 또한 어려워진다.**

    <br/>

### ✔️  Props Drilling을 해결하는 전략

- 1. **전역 상태관리 라이브러리 사용**

  - 3주차 생각과제에서 다뤘던 `Redux`, `Mobx`, `Recoil` 과 같은 상태관리 라이브러리 혹은 React에서 제공하는 Context API를 활용하여 props drilling으로 발생하는 문제를 해결 가능하다.
  - ‘전역 상태’라는 말에서 알 수 있듯이, 전역 상태관리 라이브러리를 사용하면 특정 컴포넌트가 아닌 중앙 State관리소에서 State를 생성하고, **State가 필요한 컴포넌트가 어디에 위치하든 상관없이 State를 불러와 사용할 수 있다는 장점**이 있다.

- **2. children을 적극적으로 사용**

  - `children` 이란?
    - 어떤 컴포넌트들은 어떤 자식 엘리먼트가 들어올지 미리 예상할 수 없는 경우가 있습니다. 범용적인 '박스'역할을 하는 sidebar혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있다. (리액트 공식 문서 설명)
    - **태그와 태그 사이의 모든 내용을 표시하기 위해 사용되는 특수한 Porops**
  - `props.children`은 주로 자식 컴포넌트 또는 html 엘리먼트가 어떻게 구성되어있는지 모르는데 화면에 표시해야 하는 경우 사용된다.

```jsx
export default function App() {
  const content = "Who needs me?";
  return (
    <div className="App">
      <First>
        <Second>
          <Third>
            <Props content={content} />
          </Third>
        </Second>
      </First>
    </div>
  );
}

function First({ children }) {
  return (
    <div>
      <h3>first</h3>;{children}
    </div>
  );
}

function Second({ children }) {
  return (
    <div>
      <h3>second</h3>;{children}
    </div>
  );
}

function Third({ children }) {
  return (
    <div>
      <h3>third</h3>;{children}
    </div>
  );
}

function Props({ content }) {
  return <div>{content}</div>;
}
```

→ 위 예제 코드와 같이 children을 활용하면 콘텐츠의 전달을 하위요소까지 보낼수있다.

- _💡 children 활용에 대해 더 알고 싶다면 이 [아티클](https://fe-developers.kakaoent.com/2021/211022-react-children-tip/) 읽어보는걸 추천합니당_

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

프로젝트의 규모가 커지고 공유해야 하는 state가 늘어나면 props drilling으로 코드가 복잡해질 수 있다. 이러한 props drilling을 해결하기 위해서 **전역 상태 관리, children**을 활용할 수 있다.
