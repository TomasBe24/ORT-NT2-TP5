<template>
  <div id="app">
    
    <HeaderComp/>
    

  </div>
</template>

<script>


import HeaderComp from './components/HeaderComp.vue'



export default {
  name: 'App',
  components: {
    
    HeaderComp,
    
  }
}
</script>

<style>
  body {
    background: #232323;
    margin: 0;
    font-family: "Montserrat", "Avenir";
  }
</style>
