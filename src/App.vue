<template>
  <div>
    <div id="div">
      <a href="/page1">page1</a>
      <a href="/page2">page2</a>
      <a href="/page3">page3</a>
    </div>
    <div id="container"></div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {}
  },
  mounted() {
    // 用es6的类写法
    /* 实现原理
      1.创建一个路由对象，实现register方法 处理location.pathname的值对应的回调函数
      2.处理首页
      3.处理其他页
    */
    class Router {
      constructor (){
        // 存储不同的path值对应的回调函数
        this.routers = {}
        this.listenPopState()
        this.listenLink()
      }
      // 监听postState,历史记录更改的时候，将触发postState事件
      listenPopState() {
        window.addEventListener('popstate', (e)=>{
          let state = e.state || {}
          let path = state.path || ''
          this.handler(path)
        })
      }

      // a链接的页面跳转
      listenLink() {
        window.addEventListener('click', (e)=>{
          let ev = e.target
          if (ev.tagName === 'A' && ev.getAttribute('href')) {
            // 阻止默认的跳转事件
            e.preventDefault()
            // 更新URL
            this.urlRefresh(ev.getAttribute('href'))
          }

        })
      }
      // path
      register (path,cb) {
        this.routers[path] = cb
      }

      // 首页
      index (cb) {
        this.routers['index'] = cb
      }

      // 更新URL
      urlRefresh (path) {
        /*
          1. 合理的js对象
          2. title, 现在的浏览器都不要写这个
          3. 一个url, 要跳转的页面
        */
        history.pushState({path},null,path)
        this.handler(path)
      }

      // 通用的回调函数
      handler (path) {
        let cb 
        cb = this.routers[path]
        cb.call(this)
      }
    }
    let router = new Router()
    let container = document.getElementById('container')
    // 回调函数
    router.index(()=>{
      container.innerHTML = '我是首页'
    })
    router.register('/page1', ()=>{
      container.innerHTML = '我是page1'
    })
    router.register('/page2', ()=>{
      container.innerHTML = '我是page2'
    })
    router.register('/page3', ()=>{
      container.innerHTML = '我是page3'
    })
    router.handler('index')
  }
}
</script>