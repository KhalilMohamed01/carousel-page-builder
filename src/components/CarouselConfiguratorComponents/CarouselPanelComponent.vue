<template>
    <div class="customize-panel">
        <div class="block-title">
            <i class="fa-solid fa-images"></i> Carousel
        </div>
        <div class="block-tools">
            <tr class="spaceUnder">
                <td class="td-label">Speed </td>
                <td>
                    <div>
                        <div style="display:inline-block" class="custom-input">
                            <input :disabled="!carouselCopy.transitionIsOn" v-model="carouselCopy.transitionDuration" type="text" autocomplete="chrome-off"
                                placeholder="" class="text-right" />
                            <span> s </span>
                        </div>
                        <div style="display:inline-block;" class="custom-switch form-check form-switch">
                            <input @change="speedHandler()" v-model="carouselCopy.transitionIsOn" class="custom-switch form-check-input" type="checkbox" role="switch" id="flexSwitchCheckDefault">
                        </div>
                    </div>
                </td>

            </tr>
            <tr class="spaceUnder">
                <td class="td-label">Transition </td>
                <td>
                    <select v-model="carouselCopy.transitionStyle" class="custom-select"
                        aria-label=".form-select-sm example">
                        <option value="none">
                            <label class="custom-select-option" for="r2">None</label>
                        </option>
                        <option value="slide">
                            <label class="custom-select-option" for="r2">Slide</label>
                        </option>
                        <option value="fade">
                            <label class="custom-select-option" for="r2">Fade</label>
                        </option>
                    </select>
                </td>
            </tr>
            <tr class="spaceUnder">
                <td class="td-label">Arrow style </td>
                <td>
                    <select v-model="carouselCopy.arrowStyle" class="custom-select"
                        aria-label=".form-select-sm example">
                        <option value="none">
                            <label class="custom-select-option" for="r2">None</label>
                        </option>
                        <option value="rounded">
                            <label class="custom-select-option" for="r2">Rounded</label>
                        </option>
                        <option value="window">
                            <label class="custom-select-option" for="r2">Window</label>
                        </option>
                        <option value="boxed">
                            <label class="custom-select-option" for="r2">Boxed</label>
                        </option>
                    </select>
                </td>
            </tr>
        </div>
    </div>
</template>

<script>
export default {
    props: ['carousel'],
    mounted() {
        this.carouselCopy = this.carousel;
    },
    data() {
        return {
            carouselCopy: {
                transitionDuration: 5,
                transitionStyle: "none",
                arrowStyle: "boxed",
            },
        };
    },

    methods:{
        speedHandler(){
            this.$emit("speedHandler")
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

.custom-input {
    border: 1px solid #000000;
    border-radius: 2px;
    background-color: #2b2b33;
    max-width: 60px;
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

.custom-switch{
margin-left:0 !important;
float:none !important;
border-radius: 3px !important;
}
</style>