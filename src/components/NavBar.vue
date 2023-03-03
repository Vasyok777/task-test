<template>
   <div class="container">
      <nav class="nav" @scroll="scrollPlace">
         <a href="#" class="logo">
            <img src="@/assets/vector/logo.svg" alt="GMT India logo">
         </a>
         <div class="nav__menu" :class="[menuOpen ? 'nav__menu-active' : '']">
            <ul class="nav__menu-list">
               <li 
                  class="nav__menu-item" 
                  v-for="item in navbars"
                  :key="item"
               >
                  <a class="nav__menu-link" :href="`#${item.href}`">{{ item.name }}</a>
               </li>
            </ul>
            <a href='#' class="button button-header">Other countries</a>
         </div>
         <div class="menu__burger" @click="setOpen">
            <img 
               src="@/assets/vector/menu-burger.svg" 
               alt="Menu burger" 
            >
         </div>
      </nav>
      <HeaderContent />
   </div>
</template>

<script>
import HeaderContent from '@/components/HeaderContent.vue'
export default {
   components: { HeaderContent },
   data(){
      return{
         menuOpen: false,
         navbars: [
            {name:'Popular Places', href: 'popular'},
            {name:'Covid-19', href: 'covid'},
            {name:'Visa requirements', href: 'requirements'},
            {name:'Embassy data', href: 'embassy'},
            {name:'Customs', href: 'customs'},
            {name:'FAQs', href: 'faqs'},
         ]
      }
   },
   methods: {
      setOpen(){
         this.menuOpen = !this.menuOpen
         document.body.classList.toggle('lock');
      },
   }
}
</script>

<style lang="scss">
@media (max-width: 1150px){
  body.lock{
    overflow: hidden;
  }
}
.logo img{
   position: relative;
   width: 122px;
   height: 55px;
   z-index: 1000;
   @media (max-width: 580px){
         width: 73px;
         height: 30px;
      }
}
.nav{
   padding-top: 44px;
   padding-left: 5px;
   display: flex;
   align-items: center;
   justify-content: space-between;
   margin-bottom: 232px;
   @media (max-width: 580px){
     margin-bottom: 70px;
    }
   @media (max-width: 414px){
    margin-bottom: 111px;
  }
   &__menu{
      display: flex;
      align-items: center;
      &-item{
        position: relative;
        &:before{
          content: '';
          position: absolute;
          bottom: -5px;
          left: 0;
          width: 0%;
          transition: all .5s ease-in;
          border-bottom: 3px solid #ff843f;
        }
        &:hover{
          &:before{
            width: 100%;
          }
        }
      }
      &-list{
         display: flex;
         column-gap: 37px;
      }
      &-link{
         font-family: 'Raleway';
         font-style: normal;
         font-weight: 700;
         font-size: 18px;
         line-height: 21px;
         text-decoration: none;
         color: #024873;
      }
   }
}
.menu__burger{
   display: none;
   &-img{
      width: 40px;
   }
}
.button-header{
  margin-left: 42.9px;
}
@media (max-width: 1250px){
   .nav{
      &__menu{
         &-list{
            column-gap: 18px;
         }
      }
   }
   .button-header{
      margin-left: 20px;
   }
}
@media (max-width: 1150px){
   .nav__menu{
      display: block;
      position: fixed;
      z-index: 400;
      width: 400px;
      height: 100vh;
      right: -100%;
      top: 0;
      background: white;
      transition: all .3s ease 0s;
      @media (max-width: 580px){
         width: 100%;
      }
      & .nav__menu-list {
         display: flex;
         flex-direction: column;
         margin-top: 140px;
         align-items: center;
      }
      & .nav__menu-item {
         margin-bottom: 30px;
      }
      & .nav__menu-link {
         font-size: 30px;
      }
      & .button-header {
         margin-left: 20px;
         margin: 0 auto;
         display: block;
         width: 206px;
      }
   }
   .nav__menu.nav__menu-active{
    display: block;
    right: 0%;
   }
   .menu__burger{
      display: block;
      position: relative;
      right: 36px;
      z-index: 1000;
      @media (max-width: 580px){
         right: 10px;
      }
      @media (max-width: 414px){
         right: -10px;
      }

      & img{
         width: 30px;
         @media (max-width: 580px){
            width: 20px;
      }
      }
   }
   
}
</style>