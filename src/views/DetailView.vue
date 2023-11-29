<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <h1>MOVIEKING<br /><em>CINEMA</em></h1>
                <nav>
                    <ul>
                        <li><a href="#">Home</a></li>
                        <li><a href="#">Schedule</a></li>
                        <li><a href="#">Movies</a></li>
                        <li><a href="#">News</a></li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>

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
                    <div class="credits">
                        <p>출연진</p>
                        <div>
                            <img src="https://image.tmdb.org/t/p/w500/oe0ydnDvQJCTbAb2r5E1asVXoCP.jpg" alt="actorimg">
                            <p class="actor">Joaquin Phoenix</p>
                        </div>
                    </div>
                    <div class="review">
                        <p>작성자</p>
                        <h2 class="content"></h2>
                    </div>
                </div>
                <div class="similar">
                    <p>비슷한 영화</p>
                    <div>
                        <img src="/" alt="">
                        <p class="title">제목</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <footer id="footer" role="contentinfo">
        <div class="container">
            <div class="footer__top">
                <div class="footer__title">MOVIEKING<br /><em>CINEMA</em></div>
                <nav class="footer__nav">
                    <ul>
                        <li><a href="#">Home</a></li>
                        <li><a href="#">Schedule</a></li>
                        <li><a href="#">Movies</a></li>
                        <li><a href="#">News</a></li>
                    </ul>
                </nav>
            </div>
            <div class="footer__bottom">
                <div class="footer__email">
                    audgns722@gmail.com
                </div>
                <div class="footer__copy">
                    <p>&copy; 2023 M.Huns. All rights reserved.</p>
                </div>
            </div>
        </div>
    </footer>
</template>

<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

export default {
    setup() {
        const movieInfo = ref({});
        const route = useRoute();

        const movieInfoFetch = (movieId) => {
            const apiKey = import.meta.env.VITE_API_KEY;
            const language = 'ko-KR'
            fetch(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`)

                .then((response) => response.json())
                .then((res) => {
                    console.log(res);
                    movieInfo.value = res;
                })
                .catch((err) => {
                    console.log(err);
                })
        };
        onMounted(() => {
            const movieId = route.params.movieId;
            movieInfoFetch(movieId);
        });
        return {
            movieInfo,
        };
    }
}


</script>

<style lang="scss">
.header__inner {
    .header__nav {
        margin: 0 30px;
        height: 100px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        h1 {
            text-align: center;
            font-family: var(--Title-font);
            line-height: 0.6;
            font-size: 3rem;

            em {
                font-size: 2.5rem;
                color: rgb(201, 32, 32);
                letter-spacing: 5px;
            }
        }

        nav {
            li {
                display: inline;

                a {
                    display: inline-block;
                    padding: 10px 20px;
                    transition: all 0.3s;

                    &:hover {
                        background-color: var(--black100);
                        color: antiquewhite;
                        border-radius: 5px;
                    }
                }
            }
        }
    }

}

.detail__intro {
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
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
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

            .desc {
                margin-bottom: 10px;
            }

            .credits {
                display: flex;
                width: 100%;
                flex-wrap: wrap;

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
                    width: 100px;
                    box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px;
                }
            }
        }
    }

}
</style>