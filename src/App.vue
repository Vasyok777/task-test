<template>
   <header class="header">
      <nav-bar></nav-bar>
   </header>
   <main class="main">
      <router-view></router-view>
   </main>
   <footer class="footer"></footer>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
export default {
  components: { NavBar },

}
</script>

<style lang="scss">
@import '@glidejs/glide/dist/css/glide.core.min.css';
@import '@/styles/index.scss';
.header{
   background-image: url(@/assets/images/bj.jpg);
   background-position: center center;
   background-repeat: no-repeat;
   background-size: cover;
   @media (max-width: 580px){
      background-position: 71% 91%;
      background-size: 166%;
   }
   @media (max-width: 414px){
    background-position: 87% 82%;
    background-size: 171%;
   }
   @media (max-width: 400px){
      background-size: 239%;
   }
}
</style>