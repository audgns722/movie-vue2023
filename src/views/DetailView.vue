<template>
    <HeaderSection />
    <section>
        <div class="detail__intro">
            <div class="container">
                <div class="left play__icon">
                    <a href="#">
                        <img :src="'https://image.tmdb.org/t/p/w500/' + movieInfo.poster_path" alt="dd">
                    </a>
                </div>
                <div class="right">
                    <h2>{{ movieInfo.title }}</h2>
                    <p>{{ movieInfo.tagline }}</p>
                    <p>설명 : {{ movieInfo.overview }}</p>
                    <p>개봉일 : {{ movieInfo.release_date }}</p>
                    <p class="rating">평점 : <em>{{ movieInfo.vote_average }}</em></p>
                    <div class="genres">
                        <p v-for="genre in movieInfo.genres" :key="genre.id">
                            {{ genre.name }}
                        </p>
                        <p class="runtime">{{ movieInfo.runtime }} 분</p>
                    </div>
                    <div class="credits scroll">
                        <div v-if="movieInfo.credits" v-for="(crewMember, index) in movieInfo.credits.crew.slice(0, 10)"
                            :key="index">
                            <img v-if="crewMember.profile_path"
                                :src="'https://image.tmdb.org/t/p/w500/' + crewMember.profile_path" alt="actorimg">
                            <img v-else src="../assets/img/noimage.png" alt="이미지 없음">
                            <p class="actor">{{ crewMember.name }}</p>
                        </div>
                    </div>
                </div>
            </div>
            <!-- <div class="bottom">
                <div class="review scroll">
                    <p>댓글</p>
                    <h2 class="content"></h2>
                </div>
                <div class="similar scroll">
                    <p>비슷한 영화</p>
                    <div>
                        <img src="/" alt="">
                        <p class="title"></p>
                    </div>
                </div>
            </div> -->
        </div>
    </section>
    <FooterSection />
</template>

<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import HeaderSection from "../components/section/HeaderSection.vue";
import FooterSection from "../components/section/FooterSection.vue";

export default {
    setup() {
        const route = useRoute();
        const movieInfo = ref({});;
        const apiKey = import.meta.env.VITE_API_KEY;

        const movieInfoFetch = async (movieId) => {
            try {
                const movieInfoResponse = await fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${apiKey}&language=ko-KR`);
                const creditsResponse = await fetch(`https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=${apiKey}`);

                const [movieInfoResult, creditsResult] = await Promise.all([movieInfoResponse.json(), creditsResponse.json()]);
                movieInfo.value = { ...movieInfoResult, credits: creditsResult };
            } catch (err) {
                console.error(err);
            }
        };



        onMounted(() => {
            const movieId = route.params.movieId;
            movieInfoFetch(movieId);
        });

        return { movieInfo };
    },
    components: { FooterSection, HeaderSection }
}


</script>

<style lang="scss">
.detail__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
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

    .bottom {
        display: flex;
        justify-content: space-between;


        .review {
            width: 48%;
            max-height: 500px;
            overflow-y: scroll;
            background-color: #18181863;
            padding: 10px 15px;

        }

        .similar {
            width: 48%;
            overflow-x: scroll;
            background-color: #18181863;
            padding: 10px 15px;
        }
    }
}
</style>