<template>
   <section class="popular" id="popular">
   <div class="container-right">
      <div class="popular-row">
         <div class="popular-row__left" >
            <h4 class="popular__title title">Porular Places</h4>
            <p class="popular-row__left-text" >Lorem ipsum dolor sit amet, consectetur adipiscing elit. Justo est, est massa est ridiculus aliquam enim. Id eget adipiscing feugiat mauris, ac non at luctus pretium. Purus, vel dui ut dolor commodo, sed. Nec blandit et tincidunt euismod diam. Egestas tellus.</p>
            <div class="popular-slider" data-da=".popular-row__right,1150">
               <div class="popular-slider__number">
                  <span class="popular-slider__number-active">
                    0{{ sliderNumber }}
                  </span>
                  <span class="popular-slider__number-length">
                    0{{ sliders.length }}
                  </span>
               </div>
               <div class="popular-slider__ranger">
                  <div 
                    class="popular-slider__progress" :style="progress">
                  </div>
               </div>
               
            </div>
         </div>
         <div class="popular-row__right">
            <div class="glide">
               <div class="glide__track" data-glide-el="track">
                  <ul class="glide__slides">
                    <li 
                      v-for="slider in sliders" class="glide__slide"  
                      :key="slider.id" 
                      :style="{transform: `translate(${(sliderNumber - 1) * offset}px, 0)`}"
                      >
                        <img 
                           class="popular-slider__img" 
                           :src="require(`@/assets/images/${slider.src}`)" 
                           :alt="slider.alt"
                        >
                        <span class="popular-slider__img-text">
                          {{ slider.city }}
                        </span>
                     </li>
                  </ul>
                  </div>
               <div class="glide__arrows" data-glide-el="controls">
                  <button 
                    class="glide__arrow glide__arrow--left" data-glide-dir="<">
                    <img src="@/assets/vector/left.svg" alt="left arrow">
                  </button>
                  <button 
                    class="glide__arrow glide__arrow--right" 
                    data-glide-dir=">">
                    <img src="@/assets/vector/right.svg" alt="right arrow">
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </template>

<script>
import Glide from '@glidejs/glide'
import { useDynamicAdapt } from '@/use/dynamicAdapt.js'
export default {
  data(){
    return{
      sliders: [
        {id: 1, src: '1.jpg', alt: 'Slider Photo 1', city: 'Agra'},
        {id: 2, src: '2.jpg', alt: 'Slider Photo 2', city: 'Agra'},
        {id: 3, src: '3.jpg', alt: 'Slider Photo 3', city: 'Agra'},
        {id: 4, src: '1.jpg', alt: 'Slider Photo 1', city: 'Agra'},
        {id: 5, src: '3.jpg', alt: 'Slider Photo 3', city: 'Agra'},
        {id: 6, src: '3.jpg', alt: 'Slider Photo 3', city: 'Agra'},
        {id: 7, src: '3.jpg', alt: 'Slider Photo 3', city: 'Agra'},
      ],
      sliderNumber: 1,
      offset: 65,
    }
  },
  computed:{
    progress(){
      return {
        width: this.progresWidth + '%',
        'margin-left': this.calcWidth
      }
    },
    progresWidth(){
      return 100 / this.sliders.length
    },
    calcWidth(){
      return ((100 * this.sliderNumber) / this.sliders.length - this.progresWidth) + '%'
    },
  },
  methods:{
    getOffset(){
      if(window.innerWidth > 320 && window.innerWidth < 400){
        this.offset = 120
        return
      }else if(window.innerWidth > 400 && window.innerWidth < 500){
        this.offset = 110
        return
      }else if(window.innerWidth > 500 && window.innerWidth < 520){
        this.offset = 110
        return
      }else if(window.innerWidth > 520 && window.innerWidth < 600){
        this.offset = 80
        return
      }else if(window.innerWidth > 767 && window.innerWidth < 1020){
        this.offset = 85
        return
      }else if(window.innerWidth > 1020 && window.innerWidth < 1100){
        this.offset = 85
        return
      }else if(window.innerWidth > 1100 && window.innerWidth < 1600){
        this.offset = 65
        return
      }
    }
  },
  mounted() {
    this.getOffset();
    window.addEventListener("resize", this.getOffset);
    const glide = new Glide(".glide", {
      type: "slider",
      gap: 20,
      perView: 3,
      focusAt: 0,
      breakpoints: {
        1150: {
          type: "slider",
          focusAt: 0,
          perView: 3,
        },
        1100: {
          focusAt: 0.3,
        },
        1020: {
          focusAt: 0.1,
        },
        450: {
          focusAt: 0.01,
          startAt: 0,
          peek: {
            before: 50,
            after: 50,
          }
        },
        400: {
          peek: {
            before: 20,
            after: 50,
          }
        }
      }
    });
    useDynamicAdapt()
    glide.on("run", () => {
      this.sliderNumber = glide._i + 1;
    });
    
    glide.mount();
  },
}
</script>

<style lang="scss">
.glide.glide--ltr.glide--slider.glide--swipeable{
   position: relative;
}
.glide__arrows{
   position: absolute;
   bottom: 64px;
   top: auto;
   right: auto;
   left: -139px;
   z-index: 300;
   @media (max-width: 1150px){
    top: -90px;
    right: 162px;
    left: auto;
    bottom: auto;
    margin-right: 4%;
   }
   @media (max-width: 1020px){
    display: none;
   }
}

.popular{
   padding-bottom: 108.25px;
   &__title{
      margin-bottom: 40px;
      @media (max-width: 414px){
        font-size: 24px;
        line-height: 29px;
        text-align: center;
        margin-bottom: 19px;
      }
   }
   &-row{
      display: flex;
      overflow: hidden;
      @media (max-width: 1150px){
       flex-direction: column;
      }
      &__left{
         padding-top: 24px;
         width: 400px;
         margin-right: 40px;
         background: #eff6f8;
         z-index: 200;
         position: relative;
         flex-shrink: 0;
         
         @media (max-width: 1400px){
            padding-left: 10px;
         }
         @media (max-width: 1150px){
            width: 100%;
            margin-right: 0px;
         }
         @media (max-width: 767px){
          text-align: center;
          margin: 0 auto;
         }
         @media (max-width: 414px){
            padding-left: 17px;
         }
         &-text{
            font-family: 'Raleway';
            font-style: normal;
            font-weight: 400;
            width: 440px;
            font-size: 18px;
            line-height: 1.166;
            color: #333333;
            margin-bottom: 79px;
            @media (max-width: 1150px){
              margin-bottom: 40px;
            }
            @media (max-width: 767px){
              width: 485px;
              margin: 0 auto;
            }
            @media (max-width: 520px){
              font-size: 16px;
              line-height: 19px;
              text-align: center;
              width: 370px;
              margin-bottom: 29px;
            }
            @media (max-width: 414px){
              text-align: center;
              width: 370px;
              margin-bottom: 29px;
            }
            @media (max-width: 410px){
              width: 290px;
              font-size: 14px;
              margin-bottom: 29px;
            }
         }
      }
      &__right{
         width: 1200px;
         flex-shrink: 0;
        // mask-image: linear-gradient(to right, transparent 0%, black 22% 200%, transparent 293%);
      }
   }
   &-slider{
      &__number{
        display: block;
         font-family: 'Raleway';
         font-style: normal;
         font-weight: 700;
         line-height: 1.1666;
         @media (max-width: 1150px){
          display: none;
         }
         &-active{
            font-size: 48px;
            color: #024873;
            margin-right: 40px;
         }
         &-length{
            font-size: 19px;
            color: #BDBDBD;
         }
      }
      &__ranger{
         width: 210px;
         height: 3px;
         background: #E0E0E0;
         border-radius: 1px;
         @media (max-width: 1150px){
          margin: 0 auto;
          height: 7px;
          width: 400px;
         }
         @media (max-width: 1020px){
          margin-left: 5%;
         }
         @media (max-width: 767px){
          margin-left: 20%;
          width: 300px;
         }
         @media (max-width: 700px){
          margin-left: 15%;
         }
         @media (max-width: 600px){
          margin-left: 10%;
         }
         @media (max-width: 500px){
          height: 3px;
          width: 217px;
          margin-left: 7%;
         }
         @media (max-width: 380px){
          margin-left: 3%;
         }
      }
      &__progress{
         height: 3px;
         background: #91AFFF;
         border-radius: 18px;
         @media (max-width: 1150px){
          height: 7px;
         }
      }

   }
   &-slider__img{
      width: 100%;
      height: 100%;
      &-text{
         opacity: 0;
         font-size: 24px;
         line-height: 28px;
         color: #FFFFFF;
         text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
         position: absolute;
         bottom: 32.75px;
         left: 32px;
      }
   }
}
.glide__slides{
   display: flex;
   align-items: center;
   padding-bottom: 40px;
   @media (max-width: 414px){
    padding-bottom: 30px;
   }
}
.glide__slide{
   position: relative;
   width: fit-content !important;
   min-width: fit-content !important;
}
.glide__slide.glide__slide img{
   border-radius: 30px;
   width: 325px;
   height: 325px;
   @media (max-width: 1100px){
    width: 300px;
    height: 300px;
   }
   @media (max-width: 767px){
    width: 310px;
    height: 310px;
   }
   @media (max-width: 520px){
    width: 280px;
    height: 280px;
   }
   @media (max-width: 450px){
    width: 239px;
    height: 239px;
   }
}
.glide__slide.glide__slide--active img{
   width: 373.75px;
   height: 373.75px;
   filter: drop-shadow(6px 10px 10px rgba(2, 72, 115, 0.2));
   border-radius: 30px;
   @media (max-width: 1100px){
    width: 350px;
    height: 350px;
   }
   @media (max-width: 767px){
    width: 335px;
    height: 335px;
   }
   @media (max-width: 520px){
    width: 310px;
    height: 310px;
   }
   @media (max-width: 450px){
    width: 275px;
    height: 275px;
   }
}
.glide__slide.glide__slide--active .popular-slider__img-text{
    opacity: 1;
}
.glide__arrow.glide__arrow--left,
.glide__arrow.glide__arrow--right{
   border: 1px solid #FF843F;
   width: 45px;
   height: 45px;
   border-radius: 50%;
   background-color: transparent;
}
.glide__arrow.glide__arrow--right{
   margin-left: 50px;
}

.glide__track {
  mask-image: linear-gradient(to right, transparent 0%, black 20% 80%, transparent 200%);
  padding-left: 135px;
  @media (max-width: 1150px){
    padding-left: 10px;
    mask-image: linear-gradient(to right, transparent 0%, black 0% 80%, transparent 200%);
  }
  @media (max-width: 1100px){
    padding-left: 10px;
    mask-image: linear-gradient(to right, transparent 0%, black 20% 80%, transparent 200%);
  }
  @media (max-width: 1020px){
    padding-left: 10px;
    mask-image: linear-gradient(to right, transparent 0%, black 10% 80%, transparent 200%);
  }
  @media (max-width: 500px){
    padding-left: 10px;
    mask-image: linear-gradient(to right, transparent 0%, black 0% 80%, transparent 200%);
  }
}

</style>