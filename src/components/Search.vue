<template>
  <form>
    <input type="search" v-model="item" list="listData" name="searchBox" id="searchBox" v-on:input="$emit('updateSearchText', $event.target.value)" placeholder="Type a Movie">
    <datalist id="listData">
      <option v-for="item in listItems" :key="item" v-bind:value="item"/>
    </datalist>
  </form>
</template>

<script>
export default {
  name: 'Search',
  props: {
    msg: String,
    listItems: Array
  },
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
