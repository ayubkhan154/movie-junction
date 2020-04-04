<template>
    <div id="app">
        <p>Start your work</p>
        <Search v-on:updateSearchText="getData" v-bind:listItems="listItems"></Search>
        <p>{{listItems}}</p>
    </div>
</template>

<script>
    import Search from './components/Search.vue'
    import axios from 'axios'

    export default {
        name: 'App',
        components: {
            Search
        },
        props: {
            searchText: String
        },
        data: () => {
            return {
                apiKey: 'e335d66d',
                responseData: Object,
                listItems: Array
            }
        },
        methods: {
            getData: function (searchText) {
                if (searchText.length > 4) {
                    console.log(searchText);
                    axios.get(`http://www.omdbapi.com/?apikey=${this.apiKey}&s=${searchText}`)
                        .then(function (response) {
                            this.responseData = response
                        }.bind(this))
                        .then(function () {
                            this.listItems = this.responseData.data.Search.map(x => x["Title"]);
                        }.bind(this));
                }
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
