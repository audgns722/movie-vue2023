<template>
    <div class="detail__Image container">
        <div class="Image__wrap">
            <div class="Image" v-for="(images, index) in movieImages.slice(0, 6)" :key="index">
                <img :src="'https://image.tmdb.org/t/p/w500' + images.file_path" :alt="images.title" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        movieImages: {
            type: Object,
            required: true
        }
    },
};
</script>

<style lang="scss">
.detail__Image{
    margin-top: 10px;
    .Image__wrap {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
        .Image {
            width: 32%;
        }
        
    }
}
</style>