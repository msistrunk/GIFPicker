<template>
  <div class='item' v-on:click='copyToClipboard(item.images.original.mp4)'>
    <video class='video' width=200 height=200 autoplay loop :title=item.title playsInline muted> 
      <source :src=item.images.original.mp4 type="video/mp4">
    </video>
    <div class="copyButton">
      <transition name="bounce" mode="out-in">
        <div :key="copyText" class="text">{{ copyText }}</div>
      </transition>
    </div>
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
      this.copyText = 'Copied!'
      setTimeout(() => {
        this.copyText = 'Copy'
      }, 2000);
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
.copyButton {
  transition: .5s ease;
  opacity: 0;
  position: absolute;
  top: 85%;
  left: 80%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  text-align: center;
}
.item:hover .video {
  opacity: 0.8;
}

.item:hover .copyButton {
  opacity: 1;
}
.text {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #e63b52;
  color: white;
  font-size: smaller;
  padding: 5px 5px;
  border-radius: 10px;
}
.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .2s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
</style>
