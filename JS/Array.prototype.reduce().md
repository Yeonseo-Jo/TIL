**[📆 2023-06-22 TIL]**

<br/>

# 📍 Array.prototype.reduce() 메서드

: 배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과 값을 반환한다.

- 형식 :`arr.reduce(callback(accumulator, currentValue, index, array), initialValue)`
  - arr : 순회하고자 하는 배열
  - accumulator : 누적되는 값 / initialValue를 설정한 경우 callback 최초 호출시 initialValue 값으로 초기화, initialValue가 없을 시 arr의 0번째 인덱스 값으로 초기화
  - currentValue : 현재 배열의 요소
  - index (생략 가능) : 현재 배열 요소의 index
  - array (생략 가능) : reduce 함수를 호출한 배열
  - initialValue (생략 가능) : callback의 최초 호출 시 accumulator 초기 값

* 예제 코드

(1) 초기값을 넣어주지 않았을 때 더하기 연산

```js
const list = [1, 2, 3, 4, 5];
const result = list.reduce((acc, cur, idx) => {
  console.log(idx, acc, cur);
  return acc + cur;
});

console.log("결과: ", result);

// 결과
1 1 2
2 3 3
3 6 4
4 10 5
결과:  15
```

-> intialValue가 설정되어 있지 않으므로 accumulator의 초기 값은 0번째 index의 값인 1이며, 1부터 순회함. 순회하면서 배열 요소의 값을 accumulator에 누적하며 callback 함수에 있는 더하기 연산을 한다.

(2) 초기 값을 넣어줬을 때 더하기 연산

```js
const list = [1, 2, 3, 4, 5];
const result = list.reduce((acc, cur, idx) => {
  console.log(idx, acc, cur);
  return acc + cur;
}, 0);

console.log("결과: ", result);

// 결과
0 0 1
1 1 2
2 3 3
3 6 4
4 10 5
결과:  15
```

-> 초기값인 0을 넣어줬으므로 accumulator는 초기값, currentValue는 배열의 첫번째 값으로 계산한다.
<br/>

<hr/>

## ☑️ TIL 한 줄 정리:

배열, 혹은 객체의 합, 차와 같은 누적 연산을 구해야 할 때 reduce() 메서드를 사용하면 반복문을 사용하지 않아도 구할 수 있다.
(별도의 변수를 선언하지 않고도 모든 요소를 체크하고 누적된 값을 출력하기 용이하다)
