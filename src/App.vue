<template>
  <div id="app">
    <Header></Header>
  </div>
</template>

<script>
import Header from './layouts/Header.vue'

export default {
  name: 'App',
  components: {
    Header
  }
}
</script>

<style>
* {
   margin: 0;
  padding: 0;
}
</style>
