**[📆 2023-06-30 TIL]**

<br/>

# 📍 Ts에서 module, import/export, declare의 의미

### 1. `module`

: `import` 또는 `export`가 있는 파일은 모듈(Module)로 취급
→ typeScript 컴파일러가 모듈 로더를 통해 실제로 불러오는 건 오로지 타입 정보뿐이다.

- `import` : 모듈에서 데이터를 불러올 때 사용
- `export` : 모듈에서 데이터를 내보낼 때 사용

### 2. `declare`

: 타입 정보가 선언되어 있음을 알림 (compiler에게 js로 빌드 될 필요 없음을 알려주는 키워드)

### 3.`.d.ts` 파일

: 선언 코드만 담긴 파일

- 구현부가 아닌 선언부만을 작성
- 즉, 일반
  코드가 아닌 선언 코드만 작성 가능하므로 최상위에 존재하는 변수, 상수, 함수, 클래스, 네임스페이스의 선언 앞에는 반드시 `declare` 혹은 `export` 가 붙어야 함.

<br/>

참고 자료

- [declare](https://velog.io/@now_me/Typescript%EC%97%90%EC%84%9C-declare%EC%9D%B4-%EB%AD%90%EC%A7%80)
- [개념 정리 된 자료](https://it-eldorado.tistory.com/127)

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

TypeScript에서 module은 import/export가 있는 파일이다. 또한 타입 정보가 선언 되어 있음을 알리는 키워드는 declare이고 이러한 declare를 사용하여 구현이 아닌 선언 코드가 담긴 파일은 .d.ts 파일로 작성한다.
