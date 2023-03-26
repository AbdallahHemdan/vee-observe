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
      <img src="https://picsum.photos/200/300" alt="image">
    </vee-observe>
  </div>
</template>

<script>
import VeeObserve from 'vee-observe';

export default {
  name: 'App',
  components: { VeeObserve },
  methods: {
    onChange (entry) {
      console.log('on change', entry);
      if (entry.isIntersecting) {
        console.log('intersecting');
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
