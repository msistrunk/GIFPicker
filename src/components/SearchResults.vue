<template>
  <div class='container'>
    <div v-for="(item) in results" :key="item.id">
      <SearchItem :item=item />
    </div>
  </div>
</template>

<script>
import SearchItem from './SearchItem.vue';

export default {
  name: 'SearchResults',
  components:{
    SearchItem
  },
  props: {
    results: Array,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    display: flex;
    flex-wrap: wrap;
    grid-template-columns: auto auto auto auto;
    justify-content: center;
  }
</style>
