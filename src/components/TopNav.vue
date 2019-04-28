<template>
  <div class="header">
    <h1>Photo Editor</h1>
    <div class="header-buttons">
      <button v-if="photo.src" class="header-buttons__remove" @click="removePhoto"></button>
      <a v-if="photo.src" :href="photo.src" class="header-buttons__download" title="Download" @click="setTitle" :download="photo.name"></a>
      <a href="https://github.com/TanyaKonopleva" class="header-buttons__github" target="_blank" title="Github"></a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    photo: {
      type: Object,
      default: ()=> {}
    }
  },
  methods: {
    setTitle() {
      this.photo.name = prompt('How to name this photo?', 'No name')
      if (!this.photo.name) return
    },
    removePhoto() {
      this.photo.src = null
    }
  }
}
</script>
<style lang="scss">
  .header {
    padding: 10px 20px;
    background: #161616;
    display: flex;
    justify-content: space-between;
    align-items: center;
    &-buttons {
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-basis: 10%;
      a {
        display: block;
        width: 40px;
        height: 40px;
      }
      &__github {
        background: url('../assets/github.svg') no-repeat center;
        background-size: contain;
      }
      &__download {
        background: url('../assets/download.svg') no-repeat center;
        background-size: contain;
      }
      &__remove {
        background: url('../assets/garbage.svg') no-repeat center;
        background-size: contain;
        height: 30px;
        width: 30px;
      }
    }
  }
</style>
