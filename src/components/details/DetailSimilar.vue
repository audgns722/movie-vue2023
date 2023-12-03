<template>
    <div class="detail__Similar">
      <div class="similar__wrap scroll container">
        <!-- 배열 순회: 처음 10개의 아이템에만 접근 -->
        <div v-for="(movie, index) in movieSimilar.slice(0, 10)" :key="index" class="similars">
          <!-- 이미지가 있을 경우에는 실제 이미지 표시 -->
          <img v-if="movie.poster_path" :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
          <!-- 이미지가 없을 경우에는 대체 이미지 표시 -->
          <img v-else src="../../assets/img/noimage.png" alt="이미지 없음">
          <div class="title">{{ movie.title }}</div>
          <div class="average">평점 : <em>{{ movie.vote_average }}</em></div>
        </div>
      </div>
    </div>
  </template>

<script>
export default {
    props: {
        movieSimilar: {
            type: Object,
            required: true
        }
    },
};</script>
<style lang="scss">
.detail__Similar{
    padding: 30px;
    width: 100%;
    .similar__wrap {
        overflow-x: scroll;
        display: flex;
        justify-content: flex-start;
        .similars{
        margin-right: 10px;
        width: 110px;
        display: flex;
        flex-direction: column;
        align-items: center;
        
        img{
            width: 100px;
            height: 150px;
        }
        .title {
            font-size: 0.8rem;
            text-align: center;
        }
        .average {
            font-size: 0.8rem;
            text-align: center;
            em {
                color: rgb(255, 73, 73);
                font-weight: 500;
            }
        }
    }
    }
    
}
</style>