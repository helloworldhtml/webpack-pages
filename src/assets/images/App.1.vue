<template>
  <div>
    <h1>this is App</h1>
    <div @click="add">添加</div>
    <ul class="ul-color">
      <li v-for="item in txt" :key="item">{{item}}</li>
    </ul>
  </div>
</template>

<script>
// https://github.com/search?q=webpack%E6%89%93%E5%8C%85%E5%A4%9A%E9%A1%B5%E9%9D%A2&type=
// import img from './assets/images/timg.jpeg'
// import './assets/styles/test.css'
import './assets/styles/global.styl'

export default {
  name: 'App',
  data () {
    return {
      txt: []
    }
  },
  methods: {
    add() {
      this.txt.push(this.txt.length)
    }
  }
}
</script>

<style lang="stylus" scoped>
h1
  color: red
  transform : translate(100px, 100px)
.ul-color
  color: red
</style>