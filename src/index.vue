<template>
    <div class="dropzone-wrapper clearfix"
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
                    <transition name="fly-top">
                        <div class="progress" v-show="item.isUploaded"></div>
                    </transition>
                    <img :src="item.data">
                    <figcaption>
                        <h5>{{ uploadList[index].name }}</h5>
                        <a class="close" @click="handleRemove(index)">移除({{ fileSize(uploadList[index].size) }})</a>
                    </figcaption>
                </figure>
            </li>
        </ul>
        <input type="file" name="file" ref="fileInput" multiple="multiple" style="display: none;"
               @change="handleChange">
        <div class="btn-group">
            <input type="button" value="上传" @click.stop="handleUpload" v-if="uploadList.length && !allUpload">
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
  const FILE_SIZE_LIMIT = 1024 * 1024 * 5; // 5MB
  const FILE_PREVIEW = 'data:image/jpeg;base64,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';

  export default {
    props: {
      url: {
        type: String,
        required: true
      }
    },

    data() {
      return {
        uploadList: [],
        previewList: [],
        allUpload: false
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
          console.log(file);
          if (file.size > FILE_SIZE_LIMIT) {
            alert(`文件${file.name},超出大小限制！`);
          } else if (file.type.indexOf('image') === -1) {
            this.previewList.push({data: FILE_PREVIEW, isUploaded: false});
            this.uploadList.push(file);
          } else {
            this.fileReader(file, (data => {
              this.previewList.push({data, isUploaded: false});
              this.uploadList.push(file);
            }));
          }
        }
        console.log(this.previewList);
      },
      handleRemove(index) {
        this.uploadList.splice(index, 1);
        this.previewList.splice(index, 1);
      },
      handleDrop(ev) {
        for (let file of ev.dataTransfer.files) {
          if (this.uploadList.some(e => e.name === file.name)) return;
          if (file.size > FILE_SIZE_LIMIT) {
            alert(`文件${file.name},超出大小限制！`);
          } else if (file.type.indexOf('image') === -1) {
            this.previewList.push({data: FILE_PREVIEW, isUploaded: false});
            this.uploadList.push(file);
          } else {
            this.fileReader(file, (data => {
              this.previewList.push({data, isUploaded: false});
              this.uploadList.push(file);
            }));
          }
        }
      },
      handleUpload() {
        if (!this.uploadList.length) {
          alert('请选择上传文件！');
          return;
        }
        if (!this.url) {
          throw new Error('url is undefined')
        }
        let count = this.uploadList.length;
        let success = 0;
        this.uploadList.forEach(e => {
          let formData = new FormData();
          formData.append('file', e);
          let xhr = new XMLHttpRequest();
          xhr.open('post', this.url, true);
          xhr.onload = () => {
            if (xhr.status >= 200 && xhr.status < 207) {
              this.previewList[success].isUploaded = true;
              success++;
              this.$emit('onProgress', success / count, e);
              if (success === count) {
                this.allUpload = true;
                this.$emit('onSuccess');
              }
            } else {
              this.$emit('onError', xhr);
            }
          };
          xhr.send(formData);
        });
      },
      handleDragEnter(ev) {
        this.$emit('dragenter');
      },
      handleDragLeave(ev) {
        this.$emit('dragleave');
      },
      fileSize(size) {
        if (size / 1024 / 1024 < 1) {
          return (size / 1024).toFixed(2) + 'KB';
        } else {
          return (size / 1024 / 1024).toFixed(2) + 'MB';
        }
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
        position: relative;
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
                position: relative;
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
                        white-space: nowrap;
                        text-overflow: ellipsis;
                        overflow: hidden;
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
                .progress {
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background-color: #56ffa1;
                    opacity: .2;
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
        .btn-group {
            position: absolute;
            left: 50%;
            bottom: 0;
            transform: translateX(-40px);
            input {
                font-size: 20px;
                width: 80px;
                border: 1px solid gray;
                transition: .4s;
                &:hover {
                    border-color: #fff;
                    background-color: gray;
                    color: #fff;
                }
            }
        }
    }

    .fly-top-enter-active, .fly-top-leave-active {
        transition: transform .2s cubic-bezier(.55, .53, .25, .94);
    }

    .fly-top-enter, .fly-top-leave-active {
        transform: translate3d(0, -100%, 0);
    }
</style>