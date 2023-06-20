**[📆 2023-06-20 TIL]**

<br/>

# 📍 Android 모바일 웹 뷰에서 input, textArea maxLength가 적용되지 않을 때

### **❓ 문제 상황** :

솝커톤 프로젝트 '표류병' 배포 후 QA를 진행하다, 안드로이드 카카오톡 인앱 브라우저 환경에서 제한 글자수에 이르렀을 때 오류가 발생하는 것을 발견했다.

<p align="center">
<img width="280" alt="KakaoTalk_Snapshot_20230620_215238" src="https://github.com/Yeonseo-Jo/TIL/assets/77691829/b789bc01-9d2e-4b7b-a1ed-1977bc4f9b8c"/>
</p>

### **✨ 해결 방법** :

구글링을 통해 안드로이드 웹 뷰에서 maxLength 설정이 안먹히는 케이스가 있음을 알 수 있었다.

value.length와 maxLength를 비교하여, maxLength보다 커지는 경우 slice 해 주는 아래와 같은 함수를 만들고 적용시켜 maxLength를 인식하지 못하는 문제를 해결할 수 있었다.

```js
function maxLengthCheck(object) {
  if (object.value.length > object.maxLength) {
    object.value = object.value.slice(0, object.maxLength);
  }
}
```

- 참고 자료 : [안드로이드 웹 뷰에서 maxlength가 안먹힐 때](https://mungmungdog.tistory.com/31)

<br/>
<hr/>

## ☑️ TIL 한 줄 정리 :

안드로이드 웹뷰 환경에서는 단순히 maxLength 설정만으로는 인식이 안되는 경우가 있으므로, 직접 maxLength를 체크하는 함수를 적용시켜 해결하자.
