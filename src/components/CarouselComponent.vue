<template>
 <div>
   <div id="carouselExampleDark" :class="{'carousel':true,'slide':carousel.transitionStyle==='slide' || carousel.transitionStyle==='fade','carousel-fade':carousel.transitionStyle==='fade'}" data-bs-ride="carousel">
  <div class="carousel-indicators" >
    <button ref="carouselButton" v-for="(slide,index) in slides" :key="slide.id" type="button" data-bs-target="#carouselExampleDark" :data-bs-slide-to="index" :class="{active:index===0}" :aria-current="index===0" ></button>
  </div>
  <div class="carousel-inner" >
    <div ref="carouselInner" @mouseover="handleFocus(slide.id)" @mouseleave="handleFocus(slide.id)" :class="{active:index===0}"  class="carousel-item " :data-bs-interval="carousel.transitionDuration * 1000"  v-for="(slide,index) in slides" :key="slide.id" >
      <img :style="'object-fit:' + slide.imgFit +';height:64vh;max-height: 64vh;'" :src="slide.imgUrl" class="d-block w-100" alt="..." @click="removeBorder()">
      <div :style="'background:rgb('+slide.column.background.R+ ','+slide.column.background.G+','+ slide.column.background.B + ','+ slide.column.background.O+ ');border:'+slide.column.border+'px solid #808080;border-radius:'+ slide.column.borderRadius +'px;'+ 'transform:translate(' + slide.X + 'em,-'+slide.Y + 'em);'" class="carousel-caption d-none d-md-block">
        <h5 contenteditable="true" @click="modifyText">{{slide.title}}</h5>
        <p  contenteditable="true" @click="modifyText">{{slide.description}}</p>
      </div>
    </div>

  </div>
              <!-- carousel previous -->
            <button  v-if="carousel.arrowStyle == 'none'" class="carousel-control-prev"  type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button  v-if="carousel.arrowStyle == 'rounded'" class="carousel-control-prev" type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="prev">
                <div class="rounded-arrow"><span class="carousel-control-prev-icon" aria-hidden="true" style="padding-left:40px"></span></div>
                <span class="visually-hidden">Previous</span>
            </button>
            <button  v-if="carousel.arrowStyle == 'window'" class="carousel-control-prev window-arrow" type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button  v-if="carousel.arrowStyle == 'boxed'" class="carousel-control-prev boxed-arrow" type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>

            <!-- carousel next -->
            <button v-if="carousel.arrowStyle == 'none'" class="carousel-control-next" type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
            <button v-if="carousel.arrowStyle == 'rounded'" class="carousel-control-next"  type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="next">
                <div class="rounded-arrow"><span class="carousel-control-next-icon" aria-hidden="true" style="padding-left:45px"></span></div>
                <span class="visually-hidden">Next</span>
            </button>
            <button v-if="carousel.arrowStyle == 'window'" class="carousel-control-next window-arrow"  type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
            <button v-if="carousel.arrowStyle == 'boxed'" class="carousel-control-next boxed-arrow"  type="button" data-bs-target="#carouselExampleDark"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
</div>
      </div>
</template>

<script>

 
export default {
    props : ['slides','carousel'],

    data(){
      return{
          count : 3
      }
    },

  methods : {
    modifyText(e){
      this.$emit('modifyText',e)
    },
    handleFocus(id){
      console.log(id)
      this.$emit('focus',id)
    },
    removeBorder(){
      this.$emit('removeBorder')
    }
  },
  watch:{
    slides : function(){
        if(this.slides.length < this.count){
      this.$refs.carouselInner[0].classList.add("active")
      this.$refs.carouselButton[0].classList.add("active")
      this.$refs.carouselButton[0].setAttribute("aria-current",true)
        }
        this.count = this.slides.length
    }
  }
}
</script>

<style scoped>
*{
  outline : none;
  color : white;
}
.slide{
  width : 100%;
}
img{
  width : 100%;
  height : 100%;
}


.div-bg{
    background: rgb(0, 0, 0,0.5);
}

.rounded-arrow{
    background: black;
    color:white;
    width:45px;
    height:45px;
    display:flex;
    align-items: center;
    text-align: center;
    border-radius:50%;
  
}

.window-arrow{
    background: black;
    color:white;
}

.boxed-arrow{ 
    background: black;
    color:white;
    width:45px;
    height:45px;
}

</style>