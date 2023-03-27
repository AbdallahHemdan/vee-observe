<template>
  <div id="app">
    <div class="large-content__wrapper">
      Scroll down to see the image
    </div>

    <vee-observe
      :root="null"
      :root-margin="'0px'"
      :threshold="0"
      :once="false"
      @on-change="onChange"
    >
      <img :src="imgSrc" />
    </vee-observe>
  </div>
</template>

<script>
import VeeObserve from './components/observer/observer.vue';

export default {
  name: 'App',
  data () {
    return {
      imgSrc: '',
    };
  },
  components: { VeeObserve },
  methods: {
    onChange (entry) {
      console.log('on change', entry);
      if (entry.isIntersecting) {
        console.log('intersecting');
        this.imgSrc = 'https://picsum.photos/200/300';
      }
    },
  },
};
</script>

<style>
.large-content__wrapper {
  height: 2000px;
  line-height: 1000px;
  text-align: center;
  font-size: 48px;
  color: #2c3e50;
  font-weight: bold;
}
</style>
