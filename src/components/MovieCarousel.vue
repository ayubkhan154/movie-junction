<template>
    <main>
        <MoviePortrait :key="poster.imdbID"
                       :poster="(poster.Poster !== 'N/A')
                           ? poster.Poster
                           : 'https://popcornusa.s3.amazonaws.com/placeholder-movieimage.png'"
                       :title="poster.Title"
                       :year="poster.Year"
                       v-for="poster in posters"/>
        <MoviePopup v-if="showModal"/>
    </main>
</template>

<script>
    import MoviePortrait from "@/components/MoviePortrait";
    import MoviePopup from "@/components/MoviePopup";

    export default {
        name: "MovieCarousel",
        components: {
            MoviePortrait,
            MoviePopup
        },
        props: {
            posters: Array,
        },
        data: () => {
            return {
                showModal: false,
                selectedItem: {}
            }
        },
        methods: {
            showPopup: () => {

            }
        }
    }
</script>

<style scoped>
    main {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
        grid-gap: 1rem;
        margin: 1em;
    }

    main div {
        width: 100%;
        height: 100%;
    }
</style>