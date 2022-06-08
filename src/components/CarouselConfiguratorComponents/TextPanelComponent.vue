<template>
                  <div class="customize-panel">
                    <div class="block-title">
                        <i class="fa-solid fa-highlighter"></i> Text
                    </div>
                    <div v-if="selectedText == null" class="block-tools "><center>Please select a text area</center></div>
                    <div v-if="selectedText != null" class="block-tools ">
                        <div id="checkboxes" class="d-inline">
                            <input  @change="changeText('fw-bold')" type="checkbox" name="rGroup" value="1" id="r1" />
                            <label class="whatever" for="r1"><i class="fa-solid fa-bold"></i></label>
                            <input  @change="changeText('fst-italic')" type="checkbox" name="rGroup" value="2" id="r2" />
                            <label class="whatever" for="r2"><i class="fa-solid fa-italic"></i></label>
                            <input  @change="changeText('text-decoration-underline')" type="checkbox" name="rGroup" value="3" id="r3" />
                            <label class="whatever" for="r3"><i class="fa-solid fa-underline"></i></label>
                            <input  @change="changeText('text-decoration-line-through')" type="checkbox" name="rGroup" value="4" id="r4" />
                            <label class="whatever" for="r4"><i class="fa-solid fa-strikethrough"></i></label>
                        </div>
                        <div id="custom-radio" class="d-inline p-2">
                            <input  @change="changeAlignement" type="radio" name="alignGroup" value="text-start" id="p1" />
                            <label class="whatever" for="p1"><i class="fa-solid fa-align-left"></i></label>
                            <input  @change="changeAlignement" type="radio" name="alignGroup" value="text-center" id="p2" />
                            <label class="whatever" for="p2"><i class="fa-solid fa-align-center"></i></label>
                            <input  @change="changeAlignement" type="radio" name="alignGroup" value="text-end" id="p3" />
                            <label class="whatever" for="p3"><i class="fa-solid fa-align-right"></i></label>
                        </div>

                        <div class="fontSettings">
                            <div class="d-inline text-start ">
                                <select  id="txtSize" @change="changeTextSize" class="custom-select"  aria-label=".form-select-sm example">
                                    pick ure size
                                    <option class="h1" value="fs-1">
                                        <label class="custom-select-option" for="r2">Display-1</label>
                                    </option>
                                    <option class="h2" value="fs-2">
                                        <label class="custom-select-option" for="r2">Display-2</label>
                                    </option>
                                    <option class="h3" value="fs-3">
                                        <label class="custom-select-option" for="r2">Display-3</label>
                                    </option>
                                    <option class="h4" value="fs-4">
                                        <label class="custom-select-option" for="r2">Display-4</label>
                                    </option>
                                    <option class="h5" value="fs-5">
                                        <label class="custom-select-option" for="r2">Display-5</label>
                                    </option>
                                </select>
                            </div>
                                <div id="checkboxes" class="d-inline p-1">
                                <input type="checkbox" name="pppGroup" value="1" id="ppp1" disabled />
                                <label class="whatever" for="ppp1"><i class="fa-solid fa-paintbrush"></i>&nbsp;<input 
                                          v-bind:value="getCurrentTextColor()"
                                          v-on:input="textColor = $event.target.value"
                                        @change="changeTextColor(textColor)"  type="color" id="choosedCo1" />
                                </label>

                            </div>
                            <div id="checkboxes" class="d-inline ">
                                <input  type="checkbox" name="fffGroup" value="1" id="n1" disabled />
                                <label class="whatever" for="n1"><i class="fa-solid fa-highlighter"></i>&nbsp;<input 
                                          v-bind:value="getCurrentTextBgColor()"
                                          v-on:input="bgColor = $event.target.value" @change="changeTextBgColor(bgColor)"   type="color" 
                                        id="choosedColonl1" /></label>

                            </div>
                </div>

            </div>
        </div>
</template>
<script>

export default {
   props:['selectedText'],
   data(){
      return {       
            textColor : '#FFFFFF',
            bgColor:'#FFFFFF',

}
},
methods:{ 
      getCurrentTextBgColor(){
      let color = "#FFFFFF";
      if(this.selectedText != null){
        if(this.selectedText.style.backgroundColor == ""){
          color = "#FFFFFF"
        }
        else {
          let text = this.selectedText.style.backgroundColor
          let string1 = text.replace('rgb(', ' ');
          let string2 = string1.replace(')', ' ');
          let rgb = string2.split(',')
          color = "#" + ((1 << 24) + (parseInt(rgb[0], 10) << 16) + (parseInt(rgb[1], 10) << 8) + parseInt(rgb[2], 10)).toString(16).slice(1);
        }
      return color
      }


    },
    getCurrentTextColor(){
      let color;
      if(this.selectedText != null){
        if(this.selectedText.style.color == ""){
          color = "#FFFFFF"
        }
        else {
          let text = this.selectedText.style.color
          let string1 = text.replace('rgb(', ' ');
          let string2 = string1.replace(')', ' ');
          let rgb = string2.split(',')
          color = "#" + ((1 << 24) + (parseInt(rgb[0], 10) << 16) + (parseInt(rgb[1], 10) << 8) + parseInt(rgb[2], 10)).toString(16).slice(1);
        }
      return color
      }


    },
      changeTextColor(a) {
            this.$emit("changeTextColor", a);
        },
           changeTextBgColor(a) {
            this.$emit("changeTextBgColor", a);
        },

        changeText(a) {
            this.$emit("changeText", a);
        },
        changeAlignement(){
            var ele = document.getElementsByName("alignGroup");
            let res;
         
             for(let i = 0; i < ele.length; i++) {
                if(ele[i].checked){
                    
                 res = ele[i].value;

                }
               
              
            }
             this.$emit("changeTextRadio",res,ele);

        },
        changeTextSize(){
            var select = document.getElementById("txtSize");
            var option = select.options[select.selectedIndex].value;
            console.log(select +''+ option)
            
             
             
            this.$emit("changeTextSize",option,select);
            }

        
  }
};

</script>

<style scoped>

.customize-panel {
  padding-top: 1px;
  background: #3e3e46;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  margin-bottom: 3px;
}

.block-title {
  background: #2b2b33;
  text-align: left;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 12px;
  letter-spacing: 1px;
  padding-left: 10px;
  border-bottom: 1px solid black;
}


.block-tools {
  text-align: left;
  padding: 5px;
}

.whatever {
  background-color: #595964;
  color: #a6a6a8;
  vertical-align: middle;
  display: inline-block;
  width: 35px;
  height: auto;
  border: 1px solid #141217;
  text-align: center;
}

.fontSettings {
    padding-top: 2px;
    text-align: left;
}

#custom-radio input[type="radio"] {
  display: none;
}

#custom-radio {
  width: fit-content;
}

#custom-radio input[type="radio"]:checked+.whatever {
  background-color: #2b2b33;
  color: #fff;
}

#custom-radio input[type="radio"]:hover+.whatever {
  color: #fff;
}


#checkboxes input[type="checkbox"] {
  display: none;
}

#checkboxes {
  width: fit-content;
}

#checkboxes input[type="checkbox"]:checked+.whatever {
  background-color: #2b2b33;
  color: #fff;
}

#checkboxes input[type="checkbox"]:hover+.whatever {
  color: #fff;
}

.custom-select {
  background: #595964;
  color: white;
}

.custom-select-option:hover {
  background: #2b2b33;
}

.custom-select-option {
  max-width: 10px;
}

/* Color Picker */

[type="color"] {
    appearance: none;
    padding: 0;
    width: 15px;
    height: 15px;
    border: none;
}

[type="color"]::-webkit-color-swatch-wrapper {
    padding: 0;
}

[type="color"]::-webkit-color-swatch {
    border: none;
}

.color-picker {
    padding: 4px 7px;
    text-align: center;
    margin-left: 20px;
    margin-top: 2px;
}

.labelcolor {
    margin-bottom: 15px;
    display: inline-block;
    margin-top: 15px;
}
</style>