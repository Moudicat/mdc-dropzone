<template>
    <div id="app">
        <h1>mdc-vue-dropzone  example</h1>
        <dropzone>
            点击或拖拽到此处上传图片
        </dropzone>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </div>
</template>

<script>
  import dropzone from '../src/index.vue';
  export default {
    name: 'app',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      };
    },
    components: {
      dropzone
    }
  }
</script>

<style lang="scss">
    #app {
        font-family: 'Avenir', "PingFang SC", "Microsoft YaHei", Helvetica, "宋体", sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    *, *::after, *::before {
        box-sizing: border-box;
    }

    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
