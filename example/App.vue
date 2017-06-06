<template>
    <div id="app">
        <h1>mdc-dropzone  example</h1>
        <dropzone
                url="http://localhost:2777/api/upload"
                :limitInMB="16"
                :limitFiles="5"
                :headers="{'X-MDC-Token': 'test 1010100010101'}"
                @onProgress="handleProgress"
                @onSuccess="handleSuccess">
            点击或拖拽到此处上传
        </dropzone>
    </div>
</template>

<script>
//  import dropzone from '../src/index.vue';
  import dropzone from 'mdc-dropzone';
  export default {
    name: 'app',
    methods: {
      handleProgress(progress, fileData) {
        console.log(progress, fileData.name);
      },
      handleSuccess(response) {
        console.log(response);
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
