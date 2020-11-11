<template>
  <div>
      <input type='text' :value='value' placeholder='Search for a GIF' @input="updateSearch($event.target.value)">
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    placeholderText: String,
    value: {
        type: String,
    },
  },
  methods: {
      updateSearch(value) {
          this.$emit('input', value)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    input[type=text] {
        border-radius:10px;
        font-size:20pt;
    }
</style>
