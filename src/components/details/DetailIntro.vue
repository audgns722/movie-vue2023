<template>
    <div class="detail__intro">
        <div class="container">
            <div class="left play__icon">
                <a href="#">
                    <img :src="'https://image.tmdb.org/t/p/w500/' + movieBasic.poster_path" alt="dd">
                </a>
            </div>
            <div class="right">
                <h2>{{ movieBasic.title }}</h2>
                <p>{{ movieBasic.tagline }}</p>
                <p>설명 : {{ movieBasic.overview }}</p>
                <p>개봉일 : {{ movieBasic.release_date }}</p>
                <p class="rating">평점 : <em>{{ movieBasic.vote_average }}</em></p>
                <div class="genres">
                    <p v-for="genre in movieBasic.genres" :key="genre.id">
                        {{ genre.name }}
                    </p>
                    <p class="runtime">{{ movieBasic.runtime }} 분</p>
                </div>
                <div class="detail__credits">
                    <div class="credits scroll">
                        <div v-for="(crew, index) in movieCredits.crew.slice(0, 5)" :key="index">
                            <img :src="'https://image.tmdb.org/t/p/w500' + crew.profile_path" :alt="crew.name">
                            <img src="../../assets/img/noimage.png" alt="이미지 없음">
                            <p class="actor">{{ movieCredits.name }}</p>
                        </div>
                    </div>
                </div>
                <div class="credit">
                </div>
            </div>
        </div>
    </div>
</div></template>

<script>
export default {
    props: {
        movieBasic: {
            type: Object,
            required: true
        },
        movieCredits: {
            type: Object,
            required: true
        },
    },
};
</script>

<style lang="scss">
.detail__intro {
    position: relative;
    padding: 30px;

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
            display: flex;
            align-items: center;
            width: 350px;

            img {
                box-shadow: rgba(0, 0, 0, 0.25) 0px 14px 28px, rgba(0, 0, 0, 0.22) 0px 10px 10px;
            }

        }

        .right {
            width: calc(100% - 390px);
            padding: 15px 20px;
            background-color: #00000032;
            border-radius: 15px;

            h2 {
                margin-top: 10px;
                margin-bottom: 20px;
                margin-left: 10px;
                font-family: var(--mainfont-gmaket);
                font-size: 30px;
                line-height: 1;
                color: rgb(255 246 167);

            }

            p {
                margin-bottom: 15px;
            }

            .rating {
                em {
                    margin-left: 5px;
                    font-family: var(--mainfont-nanum);
                    color: rgb(255 73 73);
                    font-size: 20px;
                    font-weight: 900;
                    line-height: 1;
                }
            }

            .genres {

                p {
                    margin-right: 5px;
                    display: inline-block;
                    padding-right: 5px;
                }

                .runtime {
                    padding-left: 10px;
                    border-left: 2px solid #fff;
                }
            }

            .desc {
                margin-bottom: 10px;
            }

        }

        .detail__credits {

            .credits {
                display: flex;
                width: 100%;
                flex-wrap: nowrap;
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
                    width: 100%;
                    margin-bottom: 20px;
                }

                img {
                    border: 1px solid #ccc;
                    width: 100px;
                    box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px;
                }
            }
        }
    }
}
</style>