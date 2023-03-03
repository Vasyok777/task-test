<template>
  <div class="header__content">
         <p class="header__content-text">
            <span class="content-basic">
               India
            </span>
            dolor sit amet, consectetur adipiscing elit
         </p>
      </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
.header__content{
   width: 588px;
   padding-bottom: 326px;
   @media (max-width: 580px){
      width: 280px;
      margin: 0 auto;
      text-align: center;
   }
   @media (max-width: 414px){
    padding-bottom: 243px;
   }
   &-text{
      font-family: "Museo Sans";
      font-weight: 900;
      font-size: 48px;
      line-height: 57.6px;
      color: #024873;
      @media (max-width: 580px){
         font-size: 26px;
         text-align: center;
         line-height: 30.6px;
      }
      @media (max-width: 414px){
        font-size: 36px;
        line-height: 43px;
      }
   }
}
.content-basic{
   color: #FF843F;
}
</style>