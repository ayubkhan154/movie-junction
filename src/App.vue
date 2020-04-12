<template>
    <div id="app">
        <img alt="Logo" src="logo2.png">
        <Search @get-posters="getPosters" @hideLoading="hideLoading" @showLoading="showLoading"/>
        <object data="spinner.svg" id="spinner" v-if="showSpinner"></object>
        <MovieCarousel :posters="posterData" v-else/>
    </div>
</template>

<script>
    import Search from '@/components/Search.vue'
    import MovieCarousel from '@/components/MovieCarousel'

    export default {
        name: 'App',
        components: {
            Search,
            MovieCarousel
        },
        data: () => {
            return {
                posterData: Array,
                showSpinner: false
            }
        },
        props: {
            searchText: String
        },
        methods: {
            getPosters: function (posters) {
                this.posterData = posters
            },
            showLoading: function () {
                this.showSpinner = true
            },
            hideLoading: function () {
                this.showSpinner = false
            }
        }
    }
</script>

<style>
    body {
        margin: 0;
        display: grid;
        height: 100vh;
    }

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;

        background-color: #0f0f0f;
        color: #2c3e50;
        margin: 0;
        padding: 0;
    }

    #spinner {
        margin-top: 3em;
    }
</style>
