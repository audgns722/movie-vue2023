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
                        <!-- <li><a href="/">Schedule</a></li>
                        <li><a href="/">Movies</a></li>
                        <li><a href="/">News</a></li> -->
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
</style>