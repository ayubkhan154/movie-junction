<template>
  <form>
    <input type="search" list="listData" name="searchBox" id="searchBox" v-on:input="getData($event.target.value)" placeholder="Type a Movie" style="padding: 1em; border: 1px solid cornflowerblue; border-radius: 0; border-top-left-radius: 4px; border-bottom-left-radius: 4px;">
    <datalist id="listData">
      <option v-for="item in listItems" :key="item.imdbID" v-bind:value="item.Title" />
    </datalist>
    <input type="submit" value="Submit" style="background-color: cornflowerblue; color: white; margin: 0; padding: 1em; border: 1px solid cornflowerblue;border-radius: 0; border-top-right-radius: 4px; border-bottom-right-radius: 4px; ">
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
    getData: function (searchText) {

      if (searchText.length > 4) {
        console.log(searchText);
        axios.get(`http://www.omdbapi.com/?apikey=${this.apiKey}&s=${searchText}`)
                .then(function (response) {
                  this.responseData = response
                }.bind(this))
                .then(function () {
                  this.listItems = this.responseData.data.Search;
                }.bind(this));
      }else{
        this.listItems = [];
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
