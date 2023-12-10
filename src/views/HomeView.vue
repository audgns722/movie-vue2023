<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';

const movies = ref([]);
const searchQuery = ref('');
const apikey = import.meta.env.VITE_API_KEY;
const currentTag = ref('latest');
const homeCredits = ref([]); // 변수 추가
const selectedMovieVideos = ref([]);
const isPopupOpen = ref(false);

const fetchMovieCredits = async (movieId) => {
  try {
    const response = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=${apikey}`);
    homeCredits.value = response.data.cast;
  } catch (err) {
    console.log(err);
  }
};


const openPopup = async (movie) => {
  const movieId = movie.id || 0; // movies 배열이 비어있을 때 0을 기본값으로 사용
  try {
    // 영화에 해당하는 비디오 정보를 가져오기
    const resMovieVideos = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/videos?api_key=${apikey}`);
    selectedMovieVideos.value = resMovieVideos.data.results;
    console.log(selectedMovieVideos);
  } catch (err) {
    console.error('Failed to fetch video data', err);
  }

  // 팝업 열기
  isPopupOpen.value = true;
};

const closePopup = () => {
  // 팝업 닫기
  isPopupOpen.value = false;
};


const homeCredit = async () => {
  try {
    const response = await axios.get(`https://api.themoviedb.org/3/movie/901362/credits?api_key=${apikey}`);
    homeCredits.value = response.data.cast; // 'cast'로 수정 // 결과를 변수에 저장
  } catch (err) {
    console.log(err);
  }
};

const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: apikey,
        language: 'ko-KR',
        query: searchQuery.value,
      }
    });
    movies.value = response.data.results;
    if (movies.value.length > 0) {
      await fetchMovieCredits(movies.value[0].id);  // 첫 번째 영화의 출연진 정보를 가져옴
    }
    
  } catch (err) {
    console.log(err);
  }
};

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular';
  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing';
      break;
    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular';
      break;
    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/top_rated';
      break;
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming';
      break;
  }
  try {
    const response = await axios.get(url, {
      params: {
        api_key: apikey,
        language: 'ko-KR',
        page: "1"
      }
    });
    console.log(response.data.results);
    movies.value = response.data.results;
    currentTag.value = category;
    if (movies.value.length > 0) {
      await fetchMovieCredits(movies.value[0].id);  // 첫 번째 영화의 출연진 정보를 가져옴
    }

  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  await fetchMovies('latest');
  await homeCredit(); // 변수 초기화
});
</script>

<template>
  <HeaderSection />
  <div v-if="movies.length > 0" class="header__intro" :style="{ backgroundImage: 'url(' + getImageUrl(movies[0].backdrop_path) + ')' }">
    <div class="container">
      <div class="left play__icon" @click="openPopup(movies[0])"><a href="#">
        <img :src="'https://image.tmdb.org/t/p/w500/' + getImageUrl(movies[0].poster_path)" alt="dd">
      </a>
      </div>
      <div v-if="isPopupOpen" class="popup-overlay">
        <div class="popup-content">
          <button @click="closePopup" class="close-button">&times;</button>
          <iframe
            v-if="selectedMovieVideos && selectedMovieVideos.length > 0"
            :src="'https://www.youtube.com/embed/' + selectedMovieVideos[0].key"
            title="YouTube video player"
            width="560"
            height="315"
            frameborder="0"
            allowfullscreen
            class="popup-iframe"
          ></iframe>
        </div>
      </div>
      <div class="right">
        <h2>{{ movies[0].title }}</h2>
        <p class="r__desc">설명 : "{{ movies[0].overview }}"</p>
        <p>개봉일 : {{ movies[0].release_date }}</p>
        <p class="rating">평점 : <em>{{ movies[0].vote_average }}</em></p>
        <p>출연진</p>
        <div class="credits scroll">
          <div v-for="(crew, index) in homeCredits.slice(0, 10)" :key="index">
            <!-- profile_path가 존재하는지 확인 -->
            <img v-if="crew.profile_path" :src="'https://image.tmdb.org/t/p/w500' + crew.profile_path"
                :alt="crew.name">
            <!-- profile_path가 없는 경우 대체 이미지를 표시 -->
            <img v-else src="../../assets/img/noimage.png" alt="이미지 없음">
            <p class="actor">{{ crew.name }}</p> <!-- 수정: movieCredits.name 대신 crew.name 사용 -->
          </div>
        </div>
      </div>
    </div>
  </div>
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
            <li><a href="#" @click="fetchMovies('latest')" :class="{ active: currentTag === 'latest' }">최신영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')" :class="{ active: currentTag === 'popular' }">인기영화</a></li>
            <li><a href="#" @click="fetchMovies('toprated')" :class="{ active: currentTag === 'toprated' }">개봉예정</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')" :class="{ active: currentTag === 'upcoming' }">최고평점</a></li>
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
      movies: [],
      homeCredits: [], // 변수 추가
    };
  },
  methods: {
    async fetchRandomMovie() {
    try {
      const randomPage = Math.floor(Math.random() * 100) + 1; // 임의의 페이지 선택
      const response = await axios.get('https://api.themoviedb.org/3/movie/popular', {
        params: {
          api_key: apikey,
          language: 'ko-KR',
          page: randomPage,
        }
      });
      const movies = response.data.results;

      // 무작위 영화 선택
      const randomIndex = Math.floor(Math.random() * movies.length);
      this.movies = [movies[randomIndex]]; // 결과를 배열로 감싸서 표시
    } catch (error) {
      console.log(error);
    }
  },
    getImageUrl(path) {
      return path ? `https://image.tmdb.org/t/p/w500${path}` : ''; // 이미지가 없는 경우 빈 문자열 반환
    },
  }
}
</script>

<style lang="scss">
.header__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background-color: #00000032;
        backdrop-filter: blur(7px);
        z-index: 1;
        filter: brightness(0.2);
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;
        gap: 1vw;
        .left {
            max-width: 350px;

            @media (max-width:800px) {
              max-width: 150px;
              display: flex;
              align-items: center;
            }
            img {
                box-shadow: rgba(0, 0, 0, 0.25) 0px 14px 28px, rgba(0, 0, 0, 0.22) 0px 10px 10px;
            }

        }

        .right {
            width: calc(100% - 350px);
            padding: 15px 20px;
            background-color: #00000032;
            border-radius: 15px;
            @media (max-width:800px) {
              width: calc(100% - 150px);
            }
            @media (max-width:400px) {
              width: 100%;
            }
            .r__desc {
                overflow: hidden;
                text-overflow: ellipsis;
                display: -webkit-box;
                -webkit-line-clamp: 4;
                -webkit-box-orient: vertical;
            }
            h2 {
                margin-top: 10px;
                margin-bottom: 20px;
                margin-left: 10px;
                font-family: var(--mainfont-gmaket);
                font-size: 1.5rem;
                line-height: 1;
                color: rgb(255 246 167);

                em {}
            }

            p {
                margin-bottom: 15px;
            }

            .rating {
                em {
                    margin-left: 5px;
                    font-family: var(--mainfont-nanum);
                    color: rgb(255 73 73);
                    font-size: 1.2rem;
                    font-weight: 900;
                    line-height: 1;
                }
            }

            .desc {
                margin-bottom: 10px;
            }

            .credits {
                display: flex;
                width: 100%;
                overflow-x: scroll;

                div {
                    display: flex;
                    flex-direction: column;
                    width: 100px;
                    margin-right: 15px;

                    .actor {
                        font-size: 1rem;
                        text-align: center;
                    }
                }

                p {
                    display: block;
                    width: 100%;
                    margin-bottom: 20px;
                }

                img {
                    width: 100px;
                    box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px;
                }
            }
        }
    }

}

.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.popup-content {
  position: relative;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 20px;
  color: white;
  background: none;
  border: none;
  cursor: pointer;
}

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
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(4, 23%);
  gap: 10px;
  margin-bottom: 3vh;

  @media (max-width: 800px) {
    grid-template-columns: repeat(3, 30%);
    
  }
  @media (max-width: 600px) {
    grid-template-columns: repeat(2, 45%);
    
  }
}
</style>
