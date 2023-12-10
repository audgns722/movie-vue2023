<template>
<div class="detail__Similar container">
    <div class="Similar__title">비슷한 영화(평점순)</div>
    <div class="similar__wrap container">
        <!-- 배열 순회: 처음 10개의 아이템에만 접근 -->
        <div v-for="(movie, index) in movieSimilar.slice(0, 10)" :key="index" class="similars">
            <!-- 이미지가 있을 경우에는 실제 이미지 표시 -->
            <a :href="'/detail/' + movie.id">
                <img v-if="movie.poster_path" :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
                    :alt="movie.title">
                <img v-else src="../../assets/img/noimage.png" alt="이미지 없음">
            </a>
            <!-- 이미지가 없을 경우에는 대체 이미지 표시 -->

            <div class="title">{{ movie.title }}</div>
            <div class="average">평점 : <em>{{ movie.vote_average }}</em></div>
        </div>
        <!-- 평점이 높은 순으로 정렬된 영화가 없을 때의 처리 -->
        <div v-if="!movieSimilar || movieSimilar.length === 0">
            평점이 높은 순으로 정렬된 영화가 없습니다.
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
};
</script>
<style lang="scss">
.detail__Similar {
    padding: 30px;
    width: 100%;

    .Similar__title {
        font-family: var(--mainfont-nanum);
        margin-bottom: 10px;
    }

    .similar__wrap {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
        gap: 10px;
        justify-items: center;
        
        .similars {

            .title {
                font-size: 1rem;
                text-align: center;
                line-height: 1;
            }

            .average {
                font-size: 1rem;
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