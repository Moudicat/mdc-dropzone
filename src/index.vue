<template>
    <div
            class="dropzone-wrapper clearfix"
            ref="dropzone"
            @click="handleWrapperClick"
            @dragover.prevent
            @dragenter="handleDragEnter"
            @dragleave="handleDragLeave"
            @drop.prevent="handleDrop">
        <slot v-if="!uploadList.length"></slot>
        <ul class="preview-list" @click.stop v-else>
            <li class="preview-wrapper" v-for="(item, index) in previewList">
                <figure>
                    <img :src="item.data">
                    <figcaption>
                        <h5>{{ uploadList[index].name }}</h5>
                        <a class="close" @click="handleRemove(index)">移除</a>
                    </figcaption>
                </figure>
            </li>
        </ul>
        <input type="file" name="file" ref="fileInput" multiple="multiple" style="display: none;"
               @change="handleChange">
    </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data() {
      return {
        uploadList: [],
        previewList: []
      };
    },

    methods: {
      fileReader(data, cbk) {
        let fr = new FileReader();
        fr.onload = (ev) => {
          cbk && cbk(ev.target.result);
        };
        fr.readAsDataURL(data);
      },
      handleWrapperClick() {
        this.$refs.fileInput.click();
      },
      handleChange(ev) {
        for (let file of ev.target.files) {
          this.uploadList.push(file);
          this.fileReader(file, (data => {
            this.previewList.push({data});
          }));
        }
      },
      handleRemove(index) {
        this.uploadList.splice(index, 1);
        this.previewList.splice(index, 1);
      },
      handleDrop(ev) {
        for (let file of ev.dataTransfer.files) {
          if (this.uploadList.some(e => e.name === file.name)) return;
          this.uploadList.push(file);
          this.fileReader(file, (data => {
            this.previewList.push({data});
          }));
        }
      },
      handleDragEnter(ev) {
        this.$emit('dragenter');
      },
      handleDragLeave(ev) {
        this.$emit('dragleave');
      }
    },

    mounted() {
      document.addEventListener('drop', (ev) => {
        ev.preventDefault();
      });
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
    @import url('./css/reset.css');

    .dropzone-wrapper {
        width: 100%;
        padding: 40px 30px;
        border: 4px dashed #cbb3c2;
        font-size: 40px;
        color: #d1d1d1;
        user-select: none;
        transition: .5s;
        background-color: #fff;
        cursor: pointer;
        &:hover {
            background-color: #e8fffd;
        }
        .preview-wrapper {
            position: relative;
            float: left;
            width: 250px;
            margin-top: 10px;
            transition: .4s;
            font-size: 20px;
            figure {
                overflow: hidden;
                width: 250px;
                height: 250px;
                img {
                    width: 250px;
                    height: 250px;
                    transition: transform .4s;
                }
                figcaption {
                    width: 100%;
                    height: 80px;
                    padding: 10px;
                    transform: translateY(0);
                    background-color: #2c3f50;
                    color: #ed4466;
                    opacity: 0;
                    transition: transform .4s, opacity .3s;
                    h5 {
                        text-align: left;
                    }
                    .close {
                        display: block;
                        margin-top: 5px;
                        border: 1px solid #eee;
                        background-color: #fff;
                        transition: .4s;
                        &:hover {
                            background-color: #636363;
                            color: #fff;
                        }
                    }
                }
            }
            &:hover {
                figure {
                    img {
                        transform: translateY(-30px);
                    }
                    figcaption {
                        transform: translateY(-100%);
                        opacity: 1;
                    }
                }
            }
        }
    }
</style>