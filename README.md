# Vuejs를 이용한 영화사이트 만들기
영화 정보를 편리하게 찾고 공유할 수 있는 플랫폼입니다. "MovieKing"라는 이름의 이 사이트에서는 사용자가 최신 인기 영화를 살펴보고, 각 영화에 대한 정보와 포스터를 확인할 수 있습니다. Vue.js의 강력한 기능을 활용하여 사용자 경험을 향상시키며, responsivity를 고려한 멋진 디자인으로 영화 팬들을 매료시킬 것입니다. MovieKing 영화 업계의 트렌드를 따라잡는 최신 영화 정보를 제공하여 사용자들에게 즐거운 시간을 선사할 것입니다.


## 셋팅
```
Vue.js - The Progressive JavaScript Framework

√ Project name: ... .
√ Package name: ... movie
√ Add TypeScript? ... No
√ Add JSX Support? ... Yes
√ Add Vue Router for Single Page Application development? ... Yes
√ Add Pinia for state management? ... No
√ Add Vitest for Unit Testing? ... No
√ Add an End-to-End Testing Solution? » No
√ Add ESLint for code quality? ... Yes
√ Add Prettier for code formatting? ... Yes

Scaffolding project in C:\Users\line\Documents\GitHub\movie-project2023...

Done. Now run:

  npm install
  npm run format
  npm run dev
```

## 제작기간


## 사용 스택


## 라이브러리 설치
`npm i sass`
`npm install axios`

## 제작 순서
- scss폴더 셋팅
- ref : ref 함수는 반응적인 데이터를 생성합니다. 이것은 컴포넌트 내에서 상태를 저장하는 데 사용, .value 속성을 통해 값을 읽거나 쓸 수 있음
    - Vue.js의 ref는 일반적으로 불변성을 가진 객체를 반환합니다. ref의 값은 .value를 통해 읽거나 쓸 수 있습니다. 값이 변경될 때 컴포넌트가 리렌더링되며, 새로운 값으로 업데이트된 상태를 반영합니다.
    - React의 useState는 배열을 반환하며, 첫 번째 요소는 현재 상태를 나타내는 값이고, 두 번째 요소는 상태를 갱신하는 함수입니다.
- onMounted : 이 훅은 컴포넌트가 마운트된 후에 실행되는 함수를 정의하는 데 사용, 컴포넌트가 화면에 나타난 직후에 어떤 동작을 수행하고 싶을 때 유용
- postman :  API 테스트 및 디버깅에 유용한 도구로서, 프로젝트 개발 중에 API 요청과 응답을 테스트하고 디버깅하는 데 사용
- v-for : 디렉티브는 배열이나 객체의 각 항목을 반복하면서 템플릿 요소를 렌더링하는 데 사용
- v-bind(또는 :) : 요소의 속성에 JavaScript 표현식을 바인딩하는 데 사용
- components 분리(HomeView) 각섹션별 불러(header. main. footer)
- postman 으로 데이터 확인후 header slider부분 이미지 영화정보 불러오기


## 트러블 슈팅

<details>
<summary></summary>

- #### 

</details>