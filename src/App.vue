<template>
    <div id="app">
        <img alt="Logo" src="logo2.png">
        <Search @get-posters="getPosters"/>
        <MovieCarousel :posters="posterData"/>
    </div>
</template>

<script>
    import Search from './components/Search.vue'
    import MovieCarousel from './components/MovieCarousel'


    export default {
        name: 'App',
        components: {
            Search,
            MovieCarousel
        },
        data: () => {
            return {
                posterData: Array,
            }
        },
        props: {
            searchText: String
        },
        methods: {
            getPosters: function (posters) {
                this.posterData = posters;
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
