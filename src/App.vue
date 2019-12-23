<template>
  <div id="app">
    <top-nav :photo="photo" />
    <editor v-if="photo.src" :photo="photo" ref="image"/>
    <loader v-else ref="loader" :photo="photo" />
  </div>
</template>

<script>
import TopNav from './components/TopNav'
import Loader from './components/Loader'
import Editor from './components/Editor'
export default {
  data() {
    return {
      photo: {
        src: null,
        name: 'No name'
      }
    }
  },
  components: { TopNav, Loader, Editor },
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
}

h1, h2 {
  margin: 0;
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

button {
  border: none;
  cursor: pointer;
  outline: none;
}
</style>
