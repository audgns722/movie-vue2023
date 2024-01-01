# Vuejs를 이용한 영화사이트 만들기

<a href="https://vue-movieking-site-project2023.netlify.app/" target="_blank">사이트 이동</a> 컨트롤 클릭해주세요

## 프로젝트 소개

MovieKing은 Vue.js의 다양한 기능을 활용하여 영화 정보를 편리하게 찾을 수 있는 플랫폼입니다.

- 최신 인기 영화 보기
  - 각 영화 목록 항목에는 영화 제목, 개봉일, 평점 등의 정보가 표시됩니다.
- 영화 정보 보기
  - 영화 목록을 클릭하면 해당 영화의 상세 정보를 볼 수 있습니다. 상세 정보에는 영화의 장르, 러닝타임, 출연진 등의 정보가 포함됩니다. 또한, 영화의 썸네일을 클릭하면 예고편을 볼 수 있는 링크도 제공됩니다.
- 영화 검색 기능
  - 영화 검색창에 영화 제목을 검색하면 관련된 결과가 출력됩니다.

## 프로젝트 구성

<details>
<summary>filetree</summary>

```
📦vue-movie-porject2023
 ┣ 📂public
 ┃ ┣ 📜favicon.svg
 ┃ ┗ 📜_redirects
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┣ 📂img
 ┃ ┃ ┃ ┣ 📂icon
 ┃ ┃ ┃ ┃ ┗ 📜play.svg
 ┃ ┃ ┃ ┗ 📜noimage.png
 ┃ ┃ ┗ 📂scss
 ┃ ┃ ┃ ┣ 📜style.scss
 ┃ ┃ ┃ ┣ 📜_common.scss
 ┃ ┃ ┃ ┣ 📜_fonts.scss
 ┃ ┃ ┃ ┣ 📜_mixin.scss
 ┃ ┃ ┃ ┣ 📜_reset.scss
 ┃ ┃ ┃ ┗ 📜_var.scss
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂details
 ┃ ┃ ┃ ┣ 📜DetailImage.vue
 ┃ ┃ ┃ ┣ 📜DetailIntro.vue
 ┃ ┃ ┃ ┗ 📜DetailSimilar.vue
 ┃ ┃ ┗ 📂section
 ┃ ┃ ┃ ┣ 📜FooterSection.vue
 ┃ ┃ ┃ ┗ 📜HeaderSection.vue
 ┃ ┣ 📂router
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂views
 ┃ ┃ ┣ 📜DetailView.vue
 ┃ ┃ ┗ 📜HomeView.vue
 ┃ ┣ 📜App.vue
 ┃ ┗ 📜main.js
 ┣ 📜.env
 ┣ 📜.eslintrc.cjs
 ┣ 📜.gitignore
 ┣ 📜.prettierrc.json
 ┣ 📜index.html
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜README.md
 ┣ 📜vite.config.js
```

</details>

## 프로젝트 목표

- Vue.js의 기본 기능을 익히고, 이를 사용하여 실제 프로젝트를 구현함으로써 실무 능력을 향상
- 영화 정보를 편리하게 찾을 수 있는 플랫폼을 제공하여 사용자들에게 즐거운 경험을 제공

## 프로젝트에 사용한 기술

- Vue.js의 ref, onMounted훅, v-for, v-bind 디렉티브를 사용했습니다.
- Sass를 사용하여 CSS 스타일을 관리했습니다.
- Axios를 사용하여 영화 정보 API를 요청했습니다.

## 프로젝트 기간

2023년 11월 28일 ~ 12월 10일

## 사용 스택

프레임워크: Vue.js
컴파일러: Vite
CSS 프레임워크: Sass
라이브러리: Axios

## 라이브러리 설치

```
npm install sass
npm install axios
```

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

## 제작 순서

1. 프로젝트 셋팅
   - Node.js, Vue.js, Vite, Sass 설치
   - 프로젝트 생성 및 초기 설정
2. scss폴더 셋팅
   - CSS 프레임워크인 Sass를 사용하기 위한 설정
3. ref 사용법 익히기
   - 컴포넌트 내에서 상태를 관리하기 위한 ref 함수 사용법 익히기
4. onMounted훅 사용법 익히기
   - 컴포넌트가 마운트된 후에 실행되는 함수인 onMounted훅 사용법 익히기
5. postman 사용법 익히기
   - API 테스트 및 디버깅에 유용한 postman 사용법 익히기
6. v-for, v-bind 디렉티브 사용법 익히기
   - 배열이나 객체의 각 항목을 반복하거나 요소의 속성에 JavaScript 표현식을 바인딩하기 위한 v-for, v-bind 디렉티브 사용법 익히기
7. components 분리
   - header, main, footer 컴포넌트로 분리하여 코드 구조 개선
8. postman으로 데이터 확인
   - API를 통해 영화 정보를 요청하여 데이터가 정상적으로 반환되는지 확인
9. env환경변수 설정

   - API 키를 환경 변수로 설정하여 보안 강화

   ### 추가내용

   - ref
     - 컴포넌트 내에서 상태를 저장하는 데 사용되는 함수
     - .value 속성을 통해 값을 읽거나 쓸 수 있음
     - Vue.js의 ref는 일반적으로 불변성을 가진 객체를 반환
   - onMounted
     - 컴포넌트가 마운트된 후에 실행되는 함수
     - 컴포넌트가 화면에 나타난 직후에 어떤 동작을 수행하고 싶을 때 사용
   - postman
     - API 테스트 및 디버깅에 유용한 도구
     - 프로젝트 개발 중에 API 요청과 응답을 테스트하고 디버깅하는 데 사용
   - v-for
     - 배열이나 객체의 각 항목을 반복하면서 템플릿 요소를 렌더링하는 데 사용
   - v-bind(또는 :)
     - 요소의 속성에 JavaScript 표현식을 바인딩하는 데 사용

## 코드 미리보가

👉 Async/Await를 사용한 API 요청

```javascript
const fetchMovies = async (category) => {
  // ...
  const response = await axios.get(url, {
    /* params */
  })
  movies.value = response.data.results
  // ...
}
```

👉 Popup 기능 구현

```javascript
const openPopup = async (movie) => {
  // ...
  isPopupOpen.value = true
}

const closePopup = () => {
  isPopupOpen.value = false
}
```

👉 onMounted 생명주기

```javascript
onMounted(async () => {
  await fetchMovies('latest')
  await homeCredit()
})
```

## 트러블 슈팅

<details>
<summary>axios로 데이터 요청 시 401 Unauthorized 오류 발생</summary>

- API 키가 올바르지 않은 경우 발생할 수 있습니다. API 키를 확인하여 올바르게 설정했는지 확인
</details>
<br />

<details>
<summary>ref를 사용 시 값이 변경되지 않는 경우</summary>

- ref의 값은 .value 속성을 통해 읽거나 쓸 수 있음 .value 속성을 통해 값을 읽거나 쓸 때 값이 변경되지 않는 경우, ref가 객체를 반환하도록 설정했는지 확인
</details>
<br />

<details>
<summary>onMounted훅을 사용 시 값이 변경되지 않는 경우</summary>

- onMounted훅은 컴포넌트가 마운트된 후에 한 번만 실행됩니다. 값을 변경하려면 컴포넌트의 data 속성이나 computed 속성을 사용하여 상태를 관리
</details>

## 프로젝트를 진행하면서 배운 내용

- Vue.js의 기본 기능을 익히는 데 도움이 되었습니다.
- 영화 정보 API를 사용하면서 API 테스트 및 디버깅에 유용한 postman을 알게 되었습니다.
