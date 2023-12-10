<template>
    <HeaderSection />
    <main>
        <DetailIntro v-if="movieBasic && movieCredits && movieVideos" :movieBasic="movieBasic" :movieCredits="movieCredits" :movieVideos="movieVideos" />
        <DetailImage v-if="movieImages" :movieImages="movieImages"/>
        <DetailSimilar v-if="movieSimilar" :movieSimilar="movieSimilar"/>
        
    </main>
    <FooterSection />
</template>

<script setup>
import HeaderSection from "@/components/section/HeaderSection.vue";
import FooterSection from "@/components/section/FooterSection.vue";
import DetailIntro from "@/components/details/DetailIntro.vue";
import DetailSimilar from "@/components/details/DetailSimilar.vue";
import DetailImage from "@/components/details/DetailImage.vue";

import { onMounted, ref } from 'vue';
import axios from 'axios';
import { useRoute } from 'vue-router';


const movieBasic = ref(null);
const movieCredits = ref(null);
const movieSimilar = ref(null);
const movieImages = ref(null);
const movieVideos = ref(null);

onMounted(async () => {
    const route = useRoute();
    const movieId = route.params.movieId;
    const apikey = import.meta.env.VITE_API_KEY;
    const language = "ko-KR";

    try {
        const resMovieBasic = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apikey}`);
        movieBasic.value = resMovieBasic.data;

        const resMovieCredits = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/credits?&api_key=${apikey}`);
        movieCredits.value = resMovieCredits.data;

        const resMovieSimilar = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/similar?language=${language}&page=1&api_key=${apikey}`);
        movieSimilar.value = resMovieSimilar.data.results;

        const resMovieImages = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/images?page=1&api_key=${apikey}`);
        movieImages.value = resMovieImages.data.backdrops;

        const resMovieVideos = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/videos?api_key=${apikey}`);
        movieVideos.value = resMovieVideos.data.results;
        console.log(movieVideos);

        // 평점이 높은 순으로 정렬
        movieSimilar.value.sort((a, b) => b.vote_average - a.vote_average);

    } catch (err) {
        console.log(err);
    }
});

</script>

<script>
export default {
  props: {
    movieId: {
      type: String, // 또는 Number, movieId의 타입에 따라서
      required: true
    }
  },
}
</script>

