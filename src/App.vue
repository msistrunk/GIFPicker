<template>
  <div id="app">
    <header>GIF Picker</header>
    <SearchInput v-model='searchInput' />
    <SearchResults v-if='results' :results='results'/>
  </div>
</template>

<script>
import SearchInput from './components/SearchInput';
import SearchResults from './components/SearchResults';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SearchInput,
    SearchResults
  },
  data(){
    return{
      searchInput: '',
      results: [],
    }
  },
  mounted () {
    // These api calls should be broken out into a helper 
    // also this api key should be hidden and referenced from env variables
    // Not all data is needed so we should also pull out only what we need
    axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2')
      .then(response => (this.results.push(response.data.data)))
    axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2')
      .then(response => (this.results.push(response.data.data)))
    axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2')
      .then(response => (this.results.push(response.data.data)))
  },
  watch: {
    searchInput: function () {
      const vm = this;
      if(vm.timeout) clearTimeout(vm.timeout);
      vm.timeout = setTimeout(() => {
        axios
          .get('https://api.giphy.com/v1/gifs/search?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2',{
            params:{
              q: vm.searchInput
            }
          })
          .then(response => {
            if(response.data.data.length > 0) vm.results = response.data.data
          })
      }, 500);
    }
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@700&display=swap');

#app {
  font-family: Oswald, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
header{
  font-size: 5em;
}
</style>
