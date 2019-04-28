<template>
  <div class="drop-zone" @dragover="dragover" @drop="drop">
    <input id="loader" type="file" @change="readFile">
    <label for="loader"></label>
  </div>
</template>
<script>
export default {
  props: {
    photo: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    readFile(file) {
      let photo = file.target.files ? file.target.files[ 0 ] : file.dataTransfer.files[ 0 ]
      let reader = new FileReader()
      reader.readAsDataURL(photo)
      reader.onloadend = () => {
        this.photo.src = reader.result
      }
    },
    dragover(e) {
      e.preventDefault()
    },
    drop(e) {
      e.preventDefault()
      this.readFile(e)
    }
  }
}
</script>
<style lang="scss">
  body {
    background: rgb(54, 54, 56);
  }
  .drop-zone {
    width: 100%;
    height: calc(100vh - 60px);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #loader {
    display: none;
    & + label {
      display: block;
      width: 50px;
      height: 50px;
      border-radius: 5px;
      background: url('/src/assets/upload.svg') no-repeat center;
      background-size: contain;
      cursor: pointer;
    }
  }
</style>
