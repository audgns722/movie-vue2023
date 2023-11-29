<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';

const movies = ref([]);
const searchQuery = ref('');

const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '32ba541f2b53cf63dc83a7c31682ce72',
        language: 'ko-KR',
        query: searchQuery.value,
      }
    });
    movies.value = response.data.results;
  } catch (err) {
    console.log(err);
  }
}

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular'
  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing'
      break;
    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular'
      break;
    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/top_rated'
      break;
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming'
      break;
  }
  try {
    const response = await axios.get(url, {
      params: {
        api_key: '32ba541f2b53cf63dc83a7c31682ce72',
        language: 'ko-KR',
        page: "1"
      }
    });
    console.log(response.data.results);
    movies.value = response.data.results;
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  // 초기 페이지 로딩 시 최신 영화를 가져옴
  await fetchMovies('latest');
});

</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">
        <div class="movie__search">
          <h2 class="blind">검색하기</h2>
          <input tpye="search" v-model="searchQuery" type="search" placeholder="검색어를 입력해주세요!" @keyup.enter="searchMovies">
          <button type="submit" @click="searchMovies">click</button>
        </div>
        <!-- movie__search -->

        <div class="movie__tag">
          <ul>
            <li><a href="#" @click="fetchMovies('latest')">최신영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')">인기영화</a></li>
            <li><a href="#" @click="fetchMovies('toprated')">개봉예정</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')">최고평점</a></li>
          </ul>
        </div>
        <!-- movie__tag -->

        <section class="movie__cont">
          <h2 class="blind">영화</h2>
          <div class="movie play__icon" v-for="movie in movies" :key="movie.id">
            <a :href="'/detail/' + movie.id">
              <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
            </a>
          </div>
        </section>
        <!-- movie__tag -->

      </div>
    </div>
  </main>
  <FooterSection />
</template>

<script>
import HeaderSection from '@/components/section/HeaderSection.vue';
import FooterSection from '@/components/section/FooterSection.vue';

export default {
  name: "MovieHomePage",
  components: {
    HeaderSection,
    FooterSection,
  },
  data() {
    return {
      movie: [],
    }
  },
  methods: {
    async search(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=32ba541f2b53cf63dc83a7c31682ce72&language=ko-KR&=${query}`);
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    },
    async tags(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=32ba541f2b53cf63dc83a7c31682ce72&language=ko-KR&=${query}`);
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    },
  }
}
</script>

<style lang="scss">
.movie__search {
  margin: 20px 10px;
  position: relative;
  color: var(--white);

  input {
    border: 1px solid #999999;
    padding: 0.5rem 1rem;
    width: 100%;
    border-radius: 5px;
    background: none;
    color: var(--white);
  }

  button {
    position: absolute;
    top: 7px;
    right: 10px;
    color: var(--white);
    background: none;
    cursor: pointer;
  }
}

.movie__tag {
  ul {
    margin: 10px;
    display: flex;

    li {
      a {
        padding: 0.5rem 1rem;
        display: inline-block;
        margin-bottom: 20px;
        margin-right: 10px;
        margin-top: 10px;
        transition: all 0.3s;
        border-radius: 5px;
        background-color: var(--black100);

        &:hover {
          background-color: #d92017;
        }

        &.active {
          background-color: #d92017;
        }
      }
    }
  }
}

.movie__cont {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

  .movie {
    width: 24%;
    margin-bottom: 1.5%;
  }
}
</style>
