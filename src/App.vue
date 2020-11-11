<template>
  <div id="app">
    <header>GIF Picker</header>
    <SearchInput v-model='searchInput' />
  </div>
</template>

<script>
import SearchInput from './components/SearchInput.vue'

export default {
  name: 'App',
  components: {
    SearchInput
  },
  data(){
    return{
      searchInput: '',
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
