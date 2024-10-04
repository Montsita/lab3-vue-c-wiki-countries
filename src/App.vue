<script setup>
import Navbar from './components/Navbar.vue'
</script>

<template>
  <section class="frame-height">
  <Navbar></Navbar>
  <div class="app">
    <div class="containerApp">
      <router-view></router-view>
    </div>    
  </div>
  </section>
</template>

<style scoped>
  .app {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 80%;
  }

  .containerApp {
    display: flex;
    flex: 1; 
    justify-content: space-evenly;
  }

  .countriesList {
    width: 300px; 
    padding: 20px; 
    overflow-y: auto;
    border-right: 1px solid #ccc; 
  }

  .frame-height{
    max-height: 100vh;
    height: 100vh;
  }
</style>