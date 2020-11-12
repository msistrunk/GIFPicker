<template>
  <div id="app">
    <header>GIF Picker</header>
    <SearchInput v-model='searchInput' />
    <p v-if='giphyError' class='error'>{{ errorText }}</p>
    <SearchResults v-if='results' :results='results'/>
    <div v-if='loading' class='loader'></div>
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
      loading: false,
      giphyError: false,
      errorText: '',
    }
  },
  mounted () {
    const vm = this;
    vm.loading = true;
    vm.giphyError = false;
    // These api calls should be broken out into a helper 
    // also this api key should be hidden and referenced from env variables
    // Not all data is needed so we should also pull out only what we need
    axios
      .all([
        axios.get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2'),
        axios.get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2'),
        axios.get('https://api.giphy.com/v1/gifs/random?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2')
      ])
      .then(responseArr => {
        vm.results.push(responseArr[0].data.data)
        vm.results.push(responseArr[1].data.data)
        vm.results.push(responseArr[2].data.data)
        vm.loading = false;
      }).catch(() => {
        vm.giphyError = true;
      })
  },
  watch: {
    searchInput: function () {
      const vm = this;
      if(vm.timeout) clearTimeout(vm.timeout);
      vm.timeout = setTimeout(() => {
        vm.loading = true;
        vm.giphyError = false;
        axios
          .get('https://api.giphy.com/v1/gifs/search?api_key=pzOvipitP62VH7uZ5TvR03vFr7NAiNN2',{
            params:{
              q: vm.searchInput
            }
          })
          .then(response => {
            if(response.data.data.length > 0) vm.results = response.data.data;
            if(response.data.pagination.total_count==0){
              vm.giphyError=true;
              vm.errorText='No results found!';
            }
            vm.loading = false;
          })
          .catch(() => {
            vm.giphyError = true;
            vm.errorText='There was an error fetching your gifs. Try again Later!'
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
.loader {
  border: 6px solid #f3f3f3;
  border-radius: 50%;
  border-top: 6px solid #e63b52;
  width: 50px;
  height: 50px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;
  margin: 25px auto;
}
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
.error{
  color: red;
}
</style>
