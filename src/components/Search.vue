<template>
    <form>
        <input @input="debounce(getData,1000)" id="searchBox" list="listData" name="searchBox" type="search"
               placeholder="Type a Movie">
        <datalist id="listData">
            <option v-for="item in listItems" :key="item.imdbID" v-bind:value="item.Title"/>
        </datalist>
        <input type="submit" value="❯">
    </form>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'Search',
        data: () => {
            return {
                apiKey: 'e335d66d',
                responseData: Object,
                listItems: Array
            }
        },
        methods: {
            getData: function () {
                let searchText = document.getElementById("searchBox").value;
                if (searchText.length === 0)
                    this.listItems = [];
                axios.get(`http://www.omdbapi.com/?apikey=${this.apiKey}&s=${searchText}&type=movie`)
                    .then(function (response) {
                        this.responseData = response
                    }.bind(this))
                    .then(function () {
                        // Add reduce to remove duplicate IMDB IDs
                        this.listItems = this.responseData.data.Search.reduce((arr, curItem) => {
                            if (!arr.find(elem => elem.imdbID === curItem.imdbID))
                                arr.push(curItem);
                            return arr;
                        }, []);
                        this.$emit('get-posters', this.listItems);
                        this.$emit('hideLoading');
                    }.bind(this));
            },

            debounce: function (func, delay) {
                this.$emit('showLoading');
                return this.debounceSearch(func, delay);
            },

            debounceSearch: function (func, delay) {
                const context = this, args = arguments;
                clearTimeout(global.timer);
                global.timer = setTimeout(() => func.apply(context, args), delay);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    form {
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        width: 100%;
    }

    form input {
        border-radius: 0;
        border: 1px solid cornflowerblue;
        padding: 0.5em 1em;
        line-height: 1.5;
        font-size: x-large;
    }

    form input:active, form input:focus {
        outline: none;
    }

    form input[type=search] {
        border-right: 0;
        border-top-left-radius: 4px;
        border-bottom-left-radius: 4px;
    }

    form input[type=submit]:hover {
        cursor: pointer;
    }

    form input[type=submit] {
        border-left: 0;
        background-color: cornflowerblue;
        color: white;
        border-top-right-radius: 4px;
        border-bottom-right-radius: 4px;
    }
</style>
