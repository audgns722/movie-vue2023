<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <a href="/">
                    <h1>MOVIEKING<br /><em>CINEMA</em></h1>
                </a>

                <nav>
                    <ul>
                        <li><a href="/">Home</a></li>
                        <li><a href="/">Schedule</a></li>
                        <li><a href="/">Movies</a></li>
                        <li><a href="/">News</a></li>
                    </ul>
                </nav>
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