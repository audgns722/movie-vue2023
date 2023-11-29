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
            <div class="header__intro"
                style="backgroundImage:url(https://image.tmdb.org/t/p/w500/f1AQhx6ZfGhPZFTVKgxG91PhEYc.jpg)">
                <div class="container">
                    <div class="left play__icon">
                        <a href="#">
                            <img src="https://image.tmdb.org/t/p/w500/cFOpMbj28ZKhXDy50mrIcLhLb8g.jpg" alt="dd">
                        </a>
                    </div>
                    <div class="right">
                        <h2>Napoleon</h2>
                        <p>설명 : "프랑스군 지휘관이었던 나폴레옹의 기원과 빠르고 냉혹하게 황제 자리에 오르게 된 이야기를 아내이자 유일한 참사랑이었던 조세핀과 맺었던 중독적이고 불안정한 관계를
                            통해 가까이서 들여다본다."</p>
                        <p>개봉일 : 2023-11-22</p>
                        <p class="rating">평점 : <em>7.5</em></p>

                        <div class="credits">
                            <p>출연진</p>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/oe0ydnDvQJCTbAb2r5E1asVXoCP.jpg" alt="actorimg">
                                <p class="actor">Joaquin Phoenix</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500//5fbvIkZ02RdcXfZHUUk4cQ9kILK.jpg" alt="actorimg">
                                <p class="actor">Vanessa Kirby</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/cM5S6jdTnurZjSLwm61rqtsliI4.jpg" alt="actorimg">
                                <p class="actor">Tahar Rahim</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/mT3BqoFUkyktXLvefQA6VxaGHJz.jpg" alt="actorimg">
                                <p class="actor">Ben Miles</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/7aT6wgl1xYfBHtW2q3oADUuAwMM.jpg" alt="actorimg">
                                <p class="actor">John Hollingworth</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/yspOPFMRWPzImc1gvO6FRtiBw6U.jpg" alt="actorimg">
                                <p class="actor">Youssef Kerkour</p>
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/w1q9MLeEsNclBWuotd3r86BVfJI.jpg" alt="actorimg">
                                <p class="actor">Davide Tucci</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

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