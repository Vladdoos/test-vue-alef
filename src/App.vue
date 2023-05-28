<template>
  <header-block/>
  <router-view/>
  <footer-block/>
</template>

<script setup>
import HeaderBlock from "@/components/headerBlock.vue";
import FooterBlock from "@/components/footerBlock.vue";
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;700&display=swap');
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
body{
  margin: auto;
}
</style>
