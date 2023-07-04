**[📆 2023-07-03 TIL]**

<br/>

# 📍 이미지 미리보기 구현하기 (FileReader vs createObjectURL)

### \* 1. FileReader

: File, Blob 객체가 저장하고 있는 바이너리 데이터를 비동기적으로 읽어주는 객체

- readAsDataURL()로 읽고, 읽기가 완료되면 onload() 실행하는 Promise 객체를 return
- onload()가 실행되면 base64 인코딩 string이 저장되고, 이 base64 형태의 string으로 미리보기 구현 가능
- <details><summary>URL 생성 결과</summary> <img width="1027" alt="Pasted Graphic 6" src="https://github.com/Yeonseo-Jo/Tattour-PreTask/assets/77691829/02feeeff-7972-4a7c-9cd1-1be32e7efe77"/></details>

### \* 2. createObjectURL

: File 또는 Blob 객체를 가리키는 고유한 URL 생성

- 고유한 URL string을 만들어 미리보기 구현 가능
- 이 URL string 객체는 Doument각 닫히기 전까지 유지됨 -> 그 전에 해제하고 싶으면 하나하나 revokeObjectURL()를 통해 해제 해야 함
- <details><summary>URL 생성 결과</summary> <img width="1027" alt="Pasted Graphic 7" src="https://github.com/Yeonseo-Jo/Tattour-PreTask/assets/77691829/13e21556-11db-49a2-9f26-5e1b04df1567"></details>

### \* 비교

- 시간 : createObjectURL은 동기적 실행(즉시 실행) / FileReader는 비동기적 실행 (시간 조금 지체 후 실행)
- 메모리 사용 : createObjectURL(hash 형태) < FileReader(base64로 인코딩된 값)
- 메모리 해제 : createObjectURL->브라우저가 닫힐 때, 수동 해제를 위해 reavokeObjectURL을 해줘야 함 / FileReader -> 가비지 컬렉터에 의해 자동 제거
- 지원 : 두 방식 모두 IE10 & 모든 모던 브라우저에서 지원 가능

- 참고자료
  - https://mieumje.tistory.com/164
  - https://developer.mozilla.org/ko/docs/Web/API/URL/createObjectURL_static
  - https://developer.mozilla.org/ko/docs/Web/API/FileReader

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

js에서 이미지 미리보기를 위한 string 형태의 URL을 생성하는 방법에는 1) FileReader 방식, 2)createObjectURL 방식이 있다. 속도, 메모리 사용 및 해제 측면을 고려하여 필요에 따라 더 좋은 방식을 택하자.
