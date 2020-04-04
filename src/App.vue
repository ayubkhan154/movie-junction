<template>
    <div id="app">
        <p>Start your work</p>
        <Search></Search>
    </div>
</template>

<script>
    import Search from './components/Search.vue'


    export default {
        name: 'App',
        components: {
            Search
        },
        props: {
            searchText: String
        },

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
