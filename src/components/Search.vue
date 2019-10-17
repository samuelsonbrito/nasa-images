<template>
  <div id="search">
    <form v-on:submit.prevent="getResult(query)">
        <input type="text" v-model="query" placeholder="Pesquise">
    </form>

    <div class="results" v-if="results">
        <div v-for="result in results" :key="result.links[0].href">
            <img v-bind:src="result.links[0].href"/>
        </div>

    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'search',
  data() {
      return {
          msg: 'Search',
          query: '',
          results: ''
      }
  },

  methods: {
      getResult(query){
          axios.get(`https://images-api.nasa.gov/search?q=${query}&media_type=image`).then(response => {
              this.results = response.data.collection.items
          })
      }
  }
}
</script>

<style>

.results img{

    height: 300px;
    margin: 10px;

}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
