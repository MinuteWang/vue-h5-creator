<template>
  <div id="app">
    <ul class="list">
      <li>点击添加元素</li>
      <li v-for="(item,i) in widgetList" @click="addWidget(item)" :key="i">
        {{item}}
      </li>
    </ul>
    <operator-pannel style="float:right"></operator-pannel>
    <div class="container" id="main-wrapper">
    </div>
  </div>
</template>

<script>
import OperatorPannel from './OperatorPannel.js'
import PageRender from './creator'
export default {
  name: 'App',
  components: {
    OperatorPannel
  },
  data() {
    return {
      wrapper: null,
      widgetList: []
    }
  },
  computed: {
    page() {
      return this.$store.state.activated_page
    }
  },
  methods: {
    addWidget(item) {
      this.page.addWidget(item)
    }
  },
  mounted() {
    new PageRender({ el: '#main-wrapper' })
    this.widgetList = Object.keys(this.page.components)
  }
}
</script>

<style lang="scss">
@import url('./style/normalize.css');
@import url('./icon/iconfont.css');
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.container {
  width: 375px;
  height: 750px;
  margin: 0 auto;
  position: relative;
  overflow: auto;
  background: url("/static/simple.jpg");
}
.list {
  cursor: pointer;
  float: left;
}
</style>
