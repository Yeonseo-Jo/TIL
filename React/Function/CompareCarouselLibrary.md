**[📆 2023-07-04 TIL]**

<br/>

# 📍 리액트의 캐러셀 라이브러리 비교 : react-slick vs Swiper

### 1. react-slick

- 기본 구조 특징 : navigator 화살표 버튼이 슬라이드 외부에, pagination bullet dots 영역이 슬라이드 외부에
  <img width="1027" alt="image" src="https://github.com/Yeonseo-Jo/Tattour-PreTask/assets/77691829/99069c19-4fad-41d4-b090-d33ec9b2f1e2">
- docs : https://react-slick.neostack.com/

### 2. Swiper

- 기본 구조 특징 : navigator 화살표 버튼이 슬라이드 내부에, pagination bullet dots 영역이 슬라이드 내부에
  <img width="908" alt="image" src="https://github.com/Yeonseo-Jo/Tattour-PreTask/assets/77691829/5ef08082-1926-4f9e-961b-b8fc16489279">
- docs : https://swiperjs.com/

#### ☑️ react-slick vs swiper 개인적인 비교

1. 뭐가 더 많이 사용되나요 ? : swiper가 더 사용량 많고, 라이브러리 업데이트 주기도 더 최근

2. 커스텀 하기 뭐가 더 어렵나요? : 둘 다 css className 뜯어 고치는거라 난이도 비슷

3. 자동 재생, 속도 조절 등 옵션 뭐가 더 많은가요? : 옵션 사항은 둘 다 비슷. 둘 다 옵션 추가로 자동 재생 쉽게 구현 가능

4. 그럼 어떨 때 뭐 쓰면 좋은가요?
   : 내가 구현해야 하는 캐러셀 구조와 비슷한 라이브러리를 사용하자! 그래야 커스텀 해야 하는 부분이 줄어든다..
   (ex. 네비게이터 버튼이 밖에 있어요 -> react-slick / 네비게이터 버튼과 페이지네이션 dot이 안쪽에 있어요 -> swiper)

<br/>
<hr/>

## ☑️ TIL 한 줄 정리:

리액트에서 캐러셀을 구현할 때 사용할 수 있는 라이브러리로는 react-slick과 swiper가 있다. 구현해야 하는 뷰의 디자인과 더 유사한 구조를 가진 라이브러리를 적절하게 사용해야 한다!
