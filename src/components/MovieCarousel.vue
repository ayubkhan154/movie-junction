<template>
    <main>
        <img :alt="poster.Title" :key="poster.imdbID"
             :src="(poster.Poster !== 'N/A') ? poster.Poster : 'https://popcornusa.s3.amazonaws.com/placeholder-movieimage.png'"
             v-for="poster in posters">
    </main>
</template>

<script>
    export default {
        name: "MovieCarousel",
        props: {
            posters: Array,
        },
    }
</script>

<style scoped>
    main {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
        grid-gap: 1rem;
        margin: 1em;
    }

    main img {
        width: 100%;
        height: auto;
        border-radius: 4px;
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.23);
        object-fit: contain;
        transition: all 0.3s;
    }

    main img:hover {
        cursor: pointer;
        transform: translateY(-4px);
        box-shadow: 0 3px 9px 0 rgba(0, 0, 0, 0.65);
    }
</style>