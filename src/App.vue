<template>
  <div id="app">
    <div class="container-fluid g-0">
      <div class="row g-0 h-100">
        <div class="col-lg-9 g-0 h-100">
          <CarouselComponent @removeBorder="removeBorder" @focus="handleFocus" @modifyText="handleText" :carousel="options.carousel" :slides="options.slides"></CarouselComponent>
        </div>
        <div class="col-lg-3 g-0 h-100">
          <CarouselConfigurator @changeTextSize="changeTextSize" @speedHandler="speedHandler" @changeTextBgColor="changeTextBgColor" @changeTextColor="changeTextColor" @removeBorder="removeBorder" @changeText="changeText" @changeTextRadio="changeTextRadio"  @addSlide="addSlide" @deleteSlide="deleteSlide" :carousel="options.carousel" :slideIndex="options.slideIndex" :slides="options.slides" :selectedText="options.selectedText"></CarouselConfigurator>
       </div>
      </div>
     
    </div>
  </div>
</template>

<script>
import CarouselComponent from './components/CarouselComponent.vue';
import CarouselConfigurator from './components/CarouselConfigurator.vue';

export default {
  name: 'App',
  components: {
    CarouselComponent,
    CarouselConfigurator
},
    data(){
      return {
       options:{
      selectedText : null,
      focusOn : null,
      count : 3,
      slideIndex : 1,
      slides : [
            {
            X:0,
            Y:0,
            id:0,
            imgUrl:"https://www.pixelstalk.net/wp-content/uploads/2016/07/Free-Download-1080p-Full-HD-Images.jpg",
            imgFit:"cover",
            title:"This a title",
            description:"Lorem ipsum dolor sit amet consectetur adipisicing elit. Nobis expedita iusto odio beatae, laborum fuga eum facere culpa minus sequi?",
            bgisOn:false,
            column:{ 
              hexcolor:"#FFFFFF",
              background:{R:"255",G:"255",B:"255",O:"0.5"},
              border:0,
              borderRadius:0,
              Shadow:"",
            }
            },
                    {
            X:0,
            Y:0,
            id:1,
            imgUrl:"https://www.pixelstalk.net/wp-content/uploads/2016/07/1080p-Full-HD-Images.jpg",
            imgFit:"cover",
            title:"This a title",
            description:"Lorem ipsum dolor sit amet consectetur adipisicing elit. Nobis expedita iusto odio beatae, laborum fuga eum facere culpa minus sequi?",
            bgisOn:false,

            column:{ 
              hexcolor:"#FFFFFF",
              background:{R:"255",G:"255",B:"255",O:"0.5"},
              border:0,
              borderRadius:0,
              Shadow:"",
            }
            },
                    {
            X:0,
            Y:0,
            id:2,
            imgUrl:"https://www.pixelstalk.net/wp-content/uploads/2016/07/1080p-Full-HD-Images-For-Desktop.jpg",
            imgFit:"cover",
            title:"This a title",
            description:"Lorem ipsum dolor sit amet consectetur adipisicing elit. Nobis expedita iusto odio beatae, laborum fuga eum facere culpa minus sequi?",
            bgisOn:false,
            column:{ 
              hexcolor:"#FFFFFF",
              background:{R:"255",G:"255",B:"255",O:"0.5"},
              border:0,
              borderRadius:0,
              Shadow:"",
            }
            },
      ],
      carousel:{ 
            transitionIsOn:true,
            transitionDuration:5,
            transitionStyle:"slide",
            arrowStyle:"none",
          },
    }
    }},
  methods : {

    speedHandler(){
      let lastSpeed=5;
      if(this.options.carousel.transitionDuration != 1800) lastSpeed = this.options.carousel.transitionDuration
      if(!this.options.carousel.transitionIsOn) this.options.carousel.transitionDuration = 1800
      else{this.options.carousel.transitionDuration = lastSpeed}
    },
    changeTextSize(a,b) {
       for(let i = 0; i < b.length; i++){
                   this.options.selectedText.classList.remove(b.options[i].value)
         }
      this.options.selectedText.classList.add(a)
    },
      changeTextRadio(a,b){
    console.log("Radio Triggred :" + this.options.selectedText);
         for(let i = 0; i < b.length; i++){
                   this.options.selectedText.classList.remove(b[i].value)
         }
    this.options.selectedText.classList.add(a)

     },

        changeTextBgColor(a)  {
       this.options.selectedText.style.backgroundColor=a      
     
     },

     changeTextColor(a)  {
       this.options.selectedText.style.color=a
    
     },


  changeText(a){
   
    this.options.selectedText.classList.toggle(a)
     },
  handleText(e){
    let lastText = this.options.selectedText;
    this.options.selectedText = e.target ;
    if(!(lastText == null)){
      lastText.classList.remove("borderText")
      e.target.classList.toggle("borderText")
    }
  },
    removeBorder(){
      this.options.selectedText.classList.remove("borderText")
  },
  handleFocus(id){
    this.options.focusOn = id
   
    this.options.slides.map(slide => {
      if(slide.id === this.options.focusOn) {
        this.options.slideIndex = this.options.slides.indexOf(slide) + 1
        return
      }
    })
  },
  addSlide(){
    const newSlide =     
          {
            X:0,
            Y:0,
            id:this.options.count,
            imgUrl:"https://www.pixelstalk.net/wp-content/uploads/2016/07/Free-Download-1080p-Full-HD-Images.jpg",
            imgFit:"cover",
            title:"This a title",
            description:" Lorem ipsum dolor sit amet consectetur adipisicing elit. Nobis expedita iusto odio beatae, laborum fuga eum facere culpa minus sequi?",         
            bgIsOn:false,
            column:{ 
              hexcolor:"#FFFFFF",
              background:{R:"255",G:"255",B:"255",O:"0.5"},
              border:0,
              borderRadius:0,
              Shadow:"",
            }
          }
          this.options.slides.push(newSlide)
          this.options.count++
  
  },
  deleteSlide(){
    this.options.slides = this.options.slides.filter(slide => slide.id != this.options.focusOn)

  }
}
}
</script>

<style>
.container-fluid{
  background-color: rgb(34, 34, 34);
}
.borderText {
  border: 2px solid cyan;
}
</style>
