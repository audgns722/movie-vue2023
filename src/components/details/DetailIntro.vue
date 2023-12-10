<template>
    <div class="detail__intro" :style="{ backgroundImage: 'url(\'https://image.tmdb.org/t/p/w500/' + movieBasic.backdrop_path + '\')' }">
        <div class="container">
            <div class="left play__icon" @click="openPopup">
                <a href="#"><img :src="'https://image.tmdb.org/t/p/w500/' + movieBasic.poster_path" alt="dd"></a>
            </div>
            <div v-if="isPopupOpen" class="popup-overlay">
                <div class="popup-content">
                    <button @click="closePopup" class="close-button">&times;</button>
                    <iframe
                    width="560"
                    height="315"
                    v-if="movieVideos && movieVideos.length > 0"
                    :src="'https://www.youtube.com/embed/' + movieVideos[0].key"
                    title="YouTube video player"
                    frameborder="0"
                    allowfullscreen
                    ></iframe>
                </div>
            </div>
            <div class="right">
                <h2>{{ movieBasic.title }}</h2>
                <!-- movieBasic.tagline이 존재하는 경우에만 표시 -->
                <p v-if="movieBasic.tagline">{{ movieBasic.tagline }}</p>
                <!-- movieBasic.overview가 존재하는 경우에만 표시, 그렇지 않으면 "제공된 내용이 없습니다." 표시 -->
                <p class="r__desc" v-if="movieBasic.overview">{{ movieBasic.overview }}</p>
                <p v-else>설명 :  제공된 정보가 없습니다.</p>
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
                        <div v-for="(crew, index) in movieCredits.crew.slice(0, 10)" :key="index">
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
    </div>
</template>


<script setup>
import { ref } from 'vue';

const isPopupOpen = ref(false);

const openPopup = () => {
  isPopupOpen.value = true;
};

const closePopup = () => {
  isPopupOpen.value = false;
};
</script>
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
        movieVideos: {
            type: Object,
            required: true
        },
    },
};
</script>

<style lang="scss">
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
        filter: brightness(0.3);
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

            @media (max-width:400px) {
              display: none;
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
            .genres {
            
                p {
                    margin-right: 10px;
                    margin-bottom: 0px;
                    display: inline-block;
                    margin-bottom: 10px;
                }

                .runtime {
                    color: rgb(255, 73, 73);
                    font-weight: 700;
                }
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
 
</style>