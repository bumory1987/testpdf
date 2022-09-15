<template>
  <haed><meta charset="UTF-8"></haed>
  <ConMan></ConMan>
 </template>

<!-- <pdf src="./static/sample.pdf" :page="1">
  <template v-slot:loading>
    loading content here...
  </template>
</pdf> -->

<script>
// import pdf from 'pdfvuer'
import ConMan from './components/ConMan.vue';

export default {
  name: 'App',
  components: {
    ConMan
  },
  setup(){
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
