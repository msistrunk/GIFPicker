<template>
  <div class='item' v-on:click='copyToClipboard(item.images.original.mp4)'>
    <video class='video' width=200 height=200 autoplay loop :title=item.title playsInline muted> 
      <source :src=item.images.original.mp4 type="video/mp4">
    </video>
  </div>
</template>

<script>
export default {
  name: 'SearchItem',
  props: {
    item: Object,
  },
  data(){
    return{
      copyText: 'Copy',
    }
  },
  methods: {
    copyToClipboard(str) {
      const el = document.createElement('textarea');
      el.value = str;
      document.body.appendChild(el);
      el.select();
      document.execCommand('copy');
      document.body.removeChild(el);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.item{
  position: relative;
  cursor: pointer;
  margin: 5px 5px 0px 5px
}
.video{
  object-fit: cover;
  border-radius: 10px;
}
</style>
