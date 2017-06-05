<template>
    <div id="app">
        <h1>mdc-dropzone  example</h1>
        <dropzone url="http://localhost:2777/api/upload" @onProgress="handleProgress" :limitInMB="16" @onSuccess="handleSuccess">
            点击或拖拽到此处上传图片
        </dropzone>
    </div>
</template>

<script>
//  import dropzone from '../src/index.vue';
  import dropzone from 'mdc-dropzone';
  export default {
    name: 'app',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      };
    },
    methods: {
      handleProgress(progress, fileData) {
        console.log(progress, fileData.name);
      },
      handleSuccess(response) {
        console.log(response);
        alert('上传完成');
      }
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
