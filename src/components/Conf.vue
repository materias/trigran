<template>
    <div class="container-fluid">
        <div class="row">
            <div class="general-view col-4">
                <div class="constructor__radio" v-for="(element, index) in mydata[selected].Svg" :key="index">
                    <svg xmlns=http://www.w3.org/2000/svg viewbox="0 0 260 250" :width="element.width" :height="element.height">
                        <rect   :x="element.x" :y="element.y" :width="element.width" :height="element.height" 
                                :fill="element.fill" :stroke="element.stroke" :fillOpacity="element.fill-opacity"/>
                    </svg>
                </div>
            </div>
            <div class="constructor col-6"> 
                <div class="constructor__radio" v-for="(element, index, ind) in mydata" :key="index">
                    <label class="form-check-label">
                    <input class="form-check-input" @change="onChangeOption()" :value="Object.keys(mydata)[ind]" v-model="selected" type="radio" name="flexRadioDefault">
                    <img class="constructor__radio-img"> 
                        <p class="constructor__radio-label">{{Object.keys(mydata)[ind]}}</p>
                    </label>
                </div>
                <div>
                    <p class="constructor__label">Размер</p>
                    <div class="constructor__radio" v-for="(element, index) in mydata[selected].Razmer" :key="index">
                        <label class="form-check-label">
                        <input class="form-check-input" @change="onChangeOption()" :value="element.value" v-model="choice" type="radio" name="flexRadioDefault">
                        <img class="constructor__radio-img"> 
                            <p class="constructor__radio-label">{{element.txt}}</p>
                        </label>
                    </div>
                    <p class="constructor__label">Открывание</p>
                    <div class="constructor__radio" v-for="(element, index) in mydata[selected].Complect" :key="index">
                        <label class="form-check-label">
                        <input class="form-check-input" @change="onChangeOption()" :value="element.value" type="radio" name="flexRadioDefault">
                        <img class="constructor__radio-img"> 
                            <p class="constructor__radio-label">{{element.complect}}</p>
                        </label>
                    </div>
                    <p class="constructor__label">Материал</p>
                    <div class="constructor__radio" v-for="(element, index) in mydata[selected].Material" :key="index">
                        <label class="form-check-label">
                        <input class="form-check-input" @change="onChangeOption()" :value="element.value" type="radio" name="flexRadioDefault">
                        <img class="constructor__radio-img"> 
                            <p class="constructor__radio-label">{{element}}</p>
                        </label>
                    </div>
                </div>
            </div>
            <div class="col">
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Conf',
    data() {
        return {
            mydata: {},
            selected: 88,
            zeroing: "ZEROING",
            parameters: {
                size: 'не выбрано',
                opening: 'не выбрано',
                color: 'не выбрано',
                accessories: 'не выбрано'
            }
        }
    },
    mounted() {
        let url = 'http://localhost:8080/data/door2104.json';
        axios.get(url)
        .then (res => {
            this.mydata = res.data
        })
        .catch (err => {
            console.log(err)
        })
    },
    methods: {
        onChangeOption(zeroing){
            if (zeroing == 'Y') {
            this.parameters.opening = 'не выбрано'
            this.parameters.color = 'не выбрано'
            this.parameters.accessories = 'не выбрано'
            }
        }
    }
}
</script>

<style scoped>
* {
    box-sizing: border-box;
    font-size: 12px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
h1 {
    margin-left: 20px;
}
.general-view {
    width: 35%;
    display: flex;
}
.constructor__label {
    margin-top: 40px;
    margin-left: 20px;
    font-weight: bold;
}
.constructor__radio {
    display: inline-block;
    margin-left: 20px;
    border: 1px dotted pink;
}
.constructor__radio-label {
    margin-left: 20px;
    margin-top: 15px;
    width: 50px;
}
.constructor__radio-img,
.constructor__radio-span {
    width: 100px;
    height: 100px;
    border-radius: 5px;
}
input[type=radio] { 
    opacity: 0;
    width: 0;
    height: 0;
}
input[type=radio] + img {
    cursor: pointer;
}
input[type=radio]:checked,
input[type=radio]:checked + img {
    outline: 4px solid rgba(53, 117, 190, .6);
}
label {
    display: block;
    cursor: pointer;
}
</style>