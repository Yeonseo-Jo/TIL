**[📆 2023-06-21 TIL]**

<br/>

# 📍 리액트에서 한국어 글자 수 실시간 표시 방법

▶︎ 구현 하고자 했던 것 : textarea(input)의 최대 글자 수를 제한하고, 실시간으로 글자 수를 표시해 주는 기능. (ex. 45/100자와 같이 표시)

<br/>

### 1. 글자 수 **실시간**으로 표시하기 : useState 사용

- useState로 실시간 글자 수를 count 해 주어 글자 수 실시간 표시를 구현 가능하다.
- onChange 이벤트 핸들러에 value의 length로 count 수를 바꾸어 주는 로직을 넣어준다.
- 예시 코드

```jsx
const [inputCount, setInputCount] = useState(0)

...

const onInputHandler = (e) => {
    setInputCount(e.target.value.length);
}
...

<Input onChange={onInputHandler} maxLength="100"/>
<p>
<span>{inputCount}</span> //실시간으로 글자 수가 표시되는 부분
<span>/100 자 </span>
</p>
```

### 2. input/textarea에서의 **한글 글자 수 제한 오류** 해결하기

- **한글은 한 글자가 2Byte, 영어는 1 Byte라는 차이가 있다.**
  -> 따라서 maxLength 속성으로 제한하고 싶은 글자 수를 주어도, 한글의 경우 한 글자씩 더 쳐지는 오류가 발생한다.

* 따라서 value의 length와 maxLength를 비교해주는 함수를 작성 해 maxLength를 넘지 않도록 조절해줘야 한다.

```jsx
const onInputHandler = (e) => {
  if (e.target.value.length > e.target.maxLength) {
    e.target.value = e.target.value.slice(0, e.target.maxLength);
  }

  ...

};
```

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

리액트에서 input(textarea)의 글자 수를 제한하고, 이를 실시간으로 카운팅 하기 위해서는 **useState로 관리해주면 된다.** 단, **한글**의 경우 글자 수 제한 오류를 방지하기 위해 직접 글자 수를 조절하는 함수 작성이 필요하다.
