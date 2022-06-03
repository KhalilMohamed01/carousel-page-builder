<template>
   <div>
        <div class="settings text-center" >
            <div class="settings-title">
                <i class="fa-solid fa-sliders"></i> Settings
            </div>
            <div class="settings-panel">
              <carousel-panel-component @speedHandler="speedHandler" :carousel="carousel"></carousel-panel-component>
              <slide-panel-component @addSlide="addSlide" @deleteSlide="deleteSlide" :slideIndex="slideIndex" :slides="slides"></slide-panel-component>
              <text-panel-component @changeTextSize="changeTextSize" :selectedText="selectedText" @changeTextBgColor="changeTextBgColor" @changeTextColor="changeTextColor" @changeText="changeText"  @changeTextRadio="changeTextRadio"></text-panel-component>
            </div>
        </div>
            </div>
  
</template>

<script>
import CarouselPanelComponent from './CarouselPanelComponent.vue'
import SlidePanelComponent from './SlidePanelComponent.vue'
import TextPanelComponent from './TextPanelComponent.vue';

export default {
    props:['carousel','slides','slideIndex','selectedText'],
    components:{
    CarouselPanelComponent,
    SlidePanelComponent,
        TextPanelComponent
},
methods:{
          changeTextColor(a) {
            this.$emit("changeTextColor", a);
        },
            changeTextBgColor(a) {
            this.$emit("changeTextBgColor", a);
            
        },
        changeText(a) {
            this.$emit("changeText", a);
        },
            changeTextRadio(a,b) {
            this.$emit("changeTextRadio", a,b);
        },
        changeTextSize(a,b) {
            this.$emit("changeTextSize", a,b);
        },
            addSlide() {
            this.$emit("addSlide");
        },
        deleteSlide() {
            this.$emit("deleteSlide");
        },
        speedHandler(){
            this.$emit("speedHandler")
        }
}
}
</script>

<style scoped>
.settings {
    height: 100vh;
    background: #2b2b33;
    text-align: left;
    color: white;
    overflow-y:auto;
}
.settings-title {
  background: #141217;
  text-transform: uppercase;
  padding: 4px;
  font-weight: bold;
  text-align: center;
  font-size: 16px;
  letter-spacing: 1px;
  border-bottom: 1px solid black;
}

.settings-panel {
  padding: 3px;
}

</style>