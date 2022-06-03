<template>
    <div class="customize-panel">
        <div class="block-title">
            <i class="fa-regular fa-images"></i> Slide ({{slideIndex}}/{{slides.length}})
            <div></div>
            <div class="deleteBtn" @click="deleteSlide"><i class="fa-solid fa-circle-minus"></i></div>
            <div class="plusBtn" @click="addSlide"><i class="fa-solid fa-circle-plus"></i></div>
        </div>
        <div class="block-tools">
            <tr class="spaceUnder">
                <td class="td-label">Image </td>
                <td>
                    <div style="max-width:150px;text-align:left;" class="custom-input">
                        <input 
                              v-model="slidesCopy[slideIndex-1].imgUrl" style="max-width:135px;" type="text" autocomplete="chrome-off" placeholder="" />
                    </div>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td class="td-label">Image size</td>
                <td>
                    <select  v-model="slidesCopy[slideIndex-1].imgFit" class="custom-select" aria-label=".form-select-sm example">
                        <option value="none">
                            <label class="custom-select-option" for="r2">None</label>
                        </option>
                        <option value="cover">
                            <label class="custom-select-option" for="r2">Cover</label>
                        </option>
                        <option value="contain">
                            <label class="custom-select-option" for="r2">Contain</label>
                        </option>
                        <option value="fill">
                            <label class="custom-select-option" for="r2">Fill</label>
                        </option>
                        <option value="scale-down">
                            <label class="custom-select-option" for="r2">Scale-down</label>
                        </option>

                    </select>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td class="td-label">Column </td>
                <td>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td>⌙ Background</td>
                <td>
                    <input @change="hex2dec(slidesCopy[slideIndex-1].column.hexcolor)" v-model="slidesCopy[slideIndex-1].column.hexcolor" type="color">
                </td>
            </tr>
            <tr class="spaceUnder">
                <td>⌙ Opacity</td>
                <td><input v-model="slidesCopy[slideIndex-1].column.background.O" min="0" max="1" step="0.01" type="range"></td>
            </tr>
            <tr class="spaceUnder">
                <td>⌙ Position(X,Y)</td>
                <td><div>
                    <div  style="margin-right:5px;display:inline-block" class="custom-input">
                         <input  v-model="slidesCopy[slideIndex-1].X" type="number" max="11" min="-11"
                            autocomplete="chrome-off" placeholder="X" class="text-right" />
                        <span>em</span>
                    </div>
                    <div style="display:inline-block" class="custom-input">
                         <input v-model="slidesCopy[slideIndex-1].Y" type="number" max="22" min="0"
                            autocomplete="chrome-off" placeholder="Y" class="text-right" />
                        <span>em</span>
                    </div>
                    </div>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td>⌙ Border</td>
                <td>
                    <div class="custom-input">
                        <input v-model="slidesCopy[slideIndex-1].column.border" type="text"
                            autocomplete="chrome-off" placeholder="" class="text-right" />
                        <span>px</span>
                    </div>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td>⌙ Corners</td>
                <td>
                    <div class="custom-input">
                        <input v-model="slidesCopy[slideIndex-1].column.borderRadius" type="text"
                            autocomplete="chrome-off" placeholder="" class="text-right" />
                        <span>px</span>
                    </div>
                </td>
            </tr>

        </div>
    </div>
</template>

<script>
export default {
    props: ['slides','slideIndex'],
    mounted() {
        this.slidesCopy = this.slides;
        this.slideIndexCopy = this.slideIndex
    },
    data() {
        return {
            slidesCopy: [{
                  imgUrl:"",
                  imgFit:"Cover",
            }
            ],
            slideIndexCopy:null,
        };
    },

    methods: {
                addSlide() {
            this.$emit("addSlide");
        },
        deleteSlide() {
            this.$emit("deleteSlide");
        },
        hex2dec(ev){
        const color = ev;
        const r = parseInt(color.substr(1,2), 16)
        const g = parseInt(color.substr(3,2), 16)
        const b = parseInt(color.substr(5,2), 16)
        console.log(`red: ${r}, green: ${g}, blue: ${b}`)
        this.slidesCopy[this.slideIndex-1].column.background.R = r;
        this.slidesCopy[this.slideIndex-1].column.background.G = g;
        this.slidesCopy[this.slideIndex-1].column.background.B = b;

        },
    },
};
</script>

<style scoped>
.plusBtn {
    background: green;
    float: right;
    padding: 4px;
    border: 1px solid #141217;
}

.plusBtn:hover {
    background: rgb(2, 72, 2);
    cursor: pointer;
}

.deleteBtn {
    background: #E0374F;
    float: right;
    padding: 4px;
    border: 1px solid #141217;
}

.deleteBtn:hover {
    background: rgb(80, 1, 1);
    cursor: pointer;
}

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

.custom-input {
    border: 1px solid #000000;
    border-radius: 2px;
    background-color: #2b2b33;
    max-width: fit-content;
    text-align: right;
}

.custom-input:hover {
    border: 1px solid #595963;
}

.custom-input>input {
    box-sizing: content-box;
    padding: 0 6px;
    border: none;
    border-radius: 0;
    background-color: transparent;
    color: inherit;
    max-width: 20px;
    outline: none;

}

.custom-input>span {
    padding: 6px;
    color: #595963;
}


.td-label {
    width: 125px;
}

tr.spaceUnder>td {
    padding-bottom: 5px;
}

.custom-select {
    background: #595964;
    color: white;
    outline: none;
    width: 150px;
}

.custom-select:hover {
    background: #595964;
    color: white;
    border: 1px solid #4e8ce3;
    outline: none;
}

.custom-select-option:hover {
    background: #2b2b33;
}

.custom-select-option {
    max-width: 10px;
}
/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}

/* Color Picker*/

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
</style>