<template>
    <HeaderSection />
    <main>
        <DetailIntro v-if="movieBasic && movieCredits" :movieBasic="movieBasic" :movieCredits="movieCredits" />
        <DetailSimilar v-if="movieSimilar" :movieSimilar="movieSimilar"/>

        <!-- <DetailReview v-if="movieReview" :movieReview="movieReview" /> -->
        <!-- <DetailCredits v-if="movieCredits" :movieCredits="movieBasic" /> -->
    </main>
    <FooterSection />
</template>

<script>
import HeaderSection from "@/components/section/HeaderSection.vue";
import FooterSection from "@/components/section/FooterSection.vue";
import DetailIntro from "@/components/details/DetailIntro.vue";
import DetailSimilar from "@/components/details/DetailSimilar.vue";

// import DetailReview from "../components/detail/DetailReview.vue";
// import DetailCredits from "@/components/details/DetailCredits.vue";


import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from 'axios';;


// DetailInfo, DetailReview, 
export default {
    name: "MovieDetailPage",

    components: { HeaderSection, DetailIntro, DetailSimilar, FooterSection,},

    setup() {
        const movieBasic = ref(null);
        const movieCredits = ref(null);
        const movieSimilar = ref(null);
        // const movieReview = ref(null);


        const route = useRoute();

        onMounted(async () => {
            const movieId = route.params.movieId;
            const apikey = import.meta.env.VITE_API_KEY;
            const language = "ko-KR";

            try {
                const resMovieBasic = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apikey}`);
                movieBasic.value = resMovieBasic.data;

                const resMovieCredits = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/credits?&api_key=${apikey}`);
                movieCredits.value = resMovieCredits.data;
                console.log(resMovieCredits)

                const resMovieSimilar = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/similar?language=${language}&page=1&api_key=${apikey}`);
                movieSimilar.value = resMovieSimilar.data.results;
                console.log(resMovieSimilar)

                // const resMovieReview = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/reviews?language=en-US&page=1&api_key=${apikey}`);
                // movieReview.value = resMovieReview.data;
                // console.log(resMovieReview)



            } catch (err) {
                console.log(err)
            }
        });
        return { movieBasic, movieCredits, movieSimilar }
    }

}

</script>