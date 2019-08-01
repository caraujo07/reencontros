<template>
  <div id="app">
    <SearchBar />
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SearchBar from './components/SearchBar/SearchBar.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    SearchBar
  }
}
</script>

<style lang="scss" src="./SCSS/main.scss">

</style>
