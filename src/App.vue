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
  },
  created() {}
}
</script>

<style lang="stylus" scoped>
h1
  color: red
  transform : translate(100px, 100px)
.ul-color
  color: red
</style>