<template>
    <main>
        <MoviePortrait :key="poster.imdbID"
                       :poster="(poster.Poster !== 'N/A')
                           ? poster.Poster
                           : 'https://popcornusa.s3.amazonaws.com/placeholder-movieimage.png'"
                       :title="poster.Title"
                       :year="poster.Year"
                       @click="showPopup(poster.imdbID)"
                       v-for="poster in posters"
        />
        <MoviePopup :item="selectedItem" @close="closeModal" v-if="showModal"/>
    </main>
</template>

<script>
    import MoviePortrait from "@/components/MoviePortrait";
    import MoviePopup from "@/components/MoviePopup";
    import axios from "axios";

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
                selectedItem: {},
                apiKey: 'e335d66d'
            }
        },
        methods: {
            showPopup: function (id) {
                axios.get(`http://www.omdbapi.com/?apikey=${this.apiKey}&i=${id}&type=Movie`)
                    .then(function (response) {
                        this.selectedItem = response.data
                    }.bind(this))
                    .then(() => this.showModal = true);
            },
            closeModal: function () {
                this.showModal = false;
            }
        }
    }
</script>

<style scoped>
    main {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(10rem, 1fr));
        grid-gap: 1rem;
        margin: 1em;
    }

    main div {
        width: 100%;
        height: 100%;
    }

    .modal-enter {
        opacity: 0;
    }

    .modal-leave-active {
        opacity: 0;
    }

    .modal-enter .modal-container,
    .modal-leave-active .modal-container {
        -webkit-transform: scale(1.1);
        transform: scale(1.1);
    }
</style>