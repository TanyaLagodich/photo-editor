<template>
  <div class="editor">
    <div class='editor__canvas'>
      <div class="editor-buttons" v-show="seen">
        <button class="editor-buttons__cancel" @click="cancelEditing"></button>
        <button class="editor-buttons__ok" @click="saveChanges"></button>
      </div>
      <img :src="photo.src" ref="image">
    </div>
    <div class="editor-actions">
      <button @click="crop" class="editor-actions__crop"></button>
      <button @click="rotateImg" class="editor-actions__rotate"></button>
      <button @click="scaleImgX" class="editor-actions__scaleX"></button>
      <button @click="scaleImgY" class="editor-actions__scaleY"></button>
    </div>
  </div>
</template>

<script>
import Cropper from 'cropperjs'

export default {
  props: {
    photo: {
      type: Object,
      efault: ()=> {}
    }
  },
  data() {
    return {
      cropper: '',
      scaleX: -1,
      scaleY: -1,
      seen: false
    }
  },
  mounted() {
    this.createCropper()
  },
  methods: {
    createCropper() {
      this.cropper = new Cropper(this.$refs.image, {
        aspectRatio: 4 / 3,
        viewMode: 1,
        autoCrop: false,
        dragMode: 'move',
        background: false,
      })
    },
    crop() {
      this.seen = true
      this.cropper.crop()
    },
    rotateImg() {
      this.cropper.rotate(90)
      this.photo.src = this.cropper.url
    },
    scaleImgX() {
      this.cropper.scaleX(this.scaleX)
      this.scaleX = this.scaleX > 0 ? -1 : 1
      this.photo.src = this.cropper.url
    },
    scaleImgY() {
      this.cropper.scaleY(this.scaleY)
      this.scaleY = this.scaleY > 0 ? -1 : 1
      this.photo.src = this.cropper.url
    },
    cancelEditing() {
      this.cropper.clear()
      this.seen = false
    },
    saveChanges() {
      this.cropper.replace(this.cropper.getCroppedCanvas().toDataURL())
      this.photo.src = this.cropper.url
      this.seen = false
    }
  }

}
</script>

<style lang="scss">
  .editor {
    height: calc(100vh - 60px);
    position: relative;
    &__canvas {
      height: 100%;
      position: relative;
    }
    &-buttons {
      padding: 10px;
      background: rgba(0, 0, 0, .4);
      z-index: 9999;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      top: 10px;
      button {
        width: 20px;
        height: 20px;
      }
      &__cancel {
        background: url('../assets/cancel.svg') no-repeat center;
        background-size: contain;
      }
      &__ok {
        margin-left: 10px;
        background: url('../assets/done-tick.svg') no-repeat center;
        background-size: contain;
      }
    }
    &-actions {
      position: absolute;
      right: 0;
      top: 50%;
      transform: translateY(-50%);
      display: flex;
      flex-direction: column;
      button {
        width: 30px;
        height: 30px;
      }
      &__save {
        background: url('../assets/save-file-option.svg') no-repeat center;
        background-size: contain;
      }
      &__crop {
        background: url('../assets/crop-symbol.svg') no-repeat center;
        background-size: contain;
      }
      &__rotate {
        background: url('../assets/refresh-button.svg') no-repeat center;
        background-size: contain;
      }
      &__scaleX {
        background: url('../assets/horizontal-resize-option.svg') no-repeat center;
        background-size: contain;
      }
      &__scaleY {
        background: url('../assets/vertical-resizing-option.svg') no-repeat center;
        background-size: contain;
      }
    }
  }
</style>
