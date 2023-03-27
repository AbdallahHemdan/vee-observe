<div align="center">
<a href="https://github.com/AbdallahHemdan/vee-observe" rel="noopener">
  
  <img width="800" alt="Vee Observe" src="https://user-images.githubusercontent.com/40190772/227812825-f5e71b1a-cc02-413e-b50b-29cbf82f486e.png">

</div>

<h3 align="center">Vee Observe</h3>

<div align="center">

[![Version Badge][npm-version-svg]][package-url]
[![GZipped size][npm-minzip-svg]][bundlephobia-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]
<a href="https://vuejs.org/"><img src="https://img.shields.io/badge/vue-2.x-brightgreen.svg"/></a>
[![GitHub contributors](https://img.shields.io/github/contributors/AbdallahHemdan/vee-observe)](https://github.com/AbdallahHemdan/vee-observe/contributors)
[![GitHub stars](https://img.shields.io/github/stars/AbdallahHemdan/vee-observe)](https://github.com/AbdallahHemdan/vee-observe/stargazers)

</div>

> Vue implementation of the [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) to tell you when an element enters or leaves the viewport.

## Features

- 📦 **Component API** - With `vee-observe` it's easier than ever to monitor elements
- ⚡️ **Optimized performance** - Reuses Intersection Observer instances where possible
- ⚙️ **Matches native API** - Intuitive to use
- 🧪 **Ready to test** - Mocks the Intersection Observer for easy testing with [Jest](https://jestjs.io/)
- 💥 **Tiny bundle** - Around **1.1kB**

## Installation

Install using [Yarn](https://yarnpkg.com):

```sh
yarn add vee-observe
```

or NPM:

```sh
npm install vee-observe --save
```

## Usage

### `vee-observe` component

```vue
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
      @not-supported="notSupported"
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
    
    notSupported () {
      console.log('not supported');
      this.imgSrc = 'https://picsum.photos/200/300';
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

```

## API

### Options

Provide these as the options argument as props on the **`<vee-observe />`** component.

| Name           | Type                         | Default     | Description |
| ---------------| -----------------------------| ----------- | ----------- |
| **root**       | `Element`                    | `document`  | The Intersection Observer interface's read-only root property identifies the Element or Document whose bounds are treated as the bounding box of the viewport for the element which is the observer's target. If the root is `null`, then the bounds of the actual document viewport are used.  |
| **rootMargin** | `string`                     | `'0px'`     | Margin around the root. Can have values similar to the CSS margin property, e.g. "10px 20px 30px 40px" (top, right, bottom, left). The values can be percentages. This set of values serves to grow or shrink each side of the root element's bounding box before computing intersections. Defaults to all zeros. |
| **threshold**  | `number` or `number[]`       | `0`         | Number between `0` and `1` indicating the percentage that should be visible before triggering. Can also be an array of numbers, to create multiple trigger points. |
| **once**       | `boolean`                    | `false`     | Only trigger the observer once. |
| **onChange**   | `(entry, unobserve) => void` | `undefined` | Call this function whenever the intersection state changes. It will receive the current `IntersectionObserverEntry` along with `unobserve` function to stop monitoring and observing the component. |
| **notSupported**   | `() => void` | `undefined` | Call this function if intersection observer is not support. |

[package-url]: https://www.npmjs.com/package/vee-observe
[npm-version-svg]: https://img.shields.io/npm/v/vee-observe.svg
[npm-minzip-svg]:
  https://img.shields.io/bundlephobia/minzip/vee-observe.svg
[bundlephobia-url]:
  https://bundlephobia.com/result?p=vee-observe
[license-image]: http://img.shields.io/npm/l/vee-observe.svg
[license-url]: LICENSE
[downloads-image]: http://img.shields.io/npm/dm/vee-observe.svg
[downloads-url]:
  http://npm-stat.com/charts.html?package=vee-observe
[test-image]:
  https://github.com/thebuilder/vee-observe/workflows/Test/badge.svg
