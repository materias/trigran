<template>
    <div>
       <h1>КОНСТРУКТОР</h1>
       <div class="container">
           <div class="general-view">
               <img src="../assets/door_icon.svg" alt="general-view" width="700px">
           </div>
           <div class="constructor">
               <div class="constructor__size">
                    <p class="constructor__label">{{mydata.COMPLECT.complect_section_6["0"].SECTION}}</p>
                    <div class="constructor__radio" v-for="(size, index) in mydata.COMPLECT.complect_section_6" :key="index">
                        <label v-if="index != zeroing">
                            <input  type="radio" 
                                    v-model="parameters.size" 
                                    :value="size.NAME"
                                    @change="onChangeOption(mydata.COMPLECT.complect_section_6.ZEROING)"> 
                            <img class="constructor__radio-img" :src="size.ICON" alt="">
                            <p class="constructor__radio-label">{{size.NAME}}</p>
                        </label>
                    </div>
               </div>
               <div class="constructor__opening">
                    <p class="constructor__label">{{mydata.COMPLECT.complect_section_7["0"].SECTION}}</p>
                    <div class="constructor__radio" v-for="(size, index) in mydata.COMPLECT.complect_section_7" :key="index">
                        <label v-if="index != zeroing">
                            <input  type="radio" 
                                    v-model="parameters.opening" 
                                    :value="size.NAME" 
                                    :name="size.NAME"
                                    @change="onChangeOption(mydata.COMPLECT.complect_section_7.ZEROING)">
                            <img class="constructor__radio-img" :src="size.ICON" alt=""> 
                            <p class="constructor__radio-label">{{size.NAME}}</p>
                        </label>
                    </div>
               </div>
               <div class="constructor__exterior">
                    <p class="constructor__label">{{mydata.COMPLECT.complect_section_8["0"].SECTION}}</p>
                    <div class="constructor__radio" v-for="(size, index) in mydata.COMPLECT.complect_section_8" :key="index">
                        <label v-if="index != zeroing">
                            <input  type="radio" 
                                    v-model="parameters.color" 
                                    :value="size.NAME" 
                                    :name="size.NAME"
                                    @change="onChangeOption(mydata.COMPLECT.complect_section_8.ZEROING)">
                            <img class="constructor__radio-img" :src="size.IMG" alt=""> 
                            <p class="constructor__radio-label">{{size.NAME}}</p>
                        </label>
                    </div>
               </div>
               <div class="constructor__accessories">
                    <p class="constructor__label">{{mydata.COMPLECT.complect_section_9["0"].SECTION}}</p>
                    <div class="constructor__radio" v-for="(size, index) in mydata.COMPLECT.complect_section_9" :key="index">
                        <label v-if="index != zeroing">
                            <input  type="radio" 
                                    v-model="parameters.accessories" 
                                    :value="size.NAME" 
                                    :name="size.NAME">
                            <img class="constructor__radio-img" :src="size.IMG" alt=""> 
                            <p class="constructor__radio-label">{{size.NAME}}</p>
                        </label>
                    </div>
               </div>
           </div>
           <div class="container__data">
               <p class="container__data-label">Ваш выбор:</p>
               <div class="container__data-parameters">
                   Размер: {{parameters.size}}
                   <br>
                   Открытие двери: {{parameters.opening}}
                   <br>
                   Цвет: {{parameters.color}}
                   <br>
                   Фурнитура: {{parameters.accessories}}
               </div>
           </div>
       </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Constructor',
    data() {
        return {
            mydata: null,
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
        let url = 'http://localhost:8080/data/kompl.json';
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
}
h1 {
    margin-left: 20px;
}
.container {
    width: 100%;
    height: 500px;
    max-width: 1800px;
    display: flex;
}
.general-view {
    width: 35%;
    display: flex;
}
.constructor__size,
.constructor__opening,
.constructor__exterior,
.constructor__accessories {
    font-size: 12px;
    margin-top: 10px;
}
.constructor__label {
    margin-left: 20px;
    font-weight: bold;
}
.constructor__radio {
    display: inline;
    margin-left: 20px;
}
.constructor__radio-label {
    margin-left: 20px;
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
    display: inline-block;
    cursor: pointer;
}
.container__data {
    margin-left: 50px;
    margin-top: 100px;
    font-size: 12px;
    width: 280px;
    height: 200px;
    box-shadow: 0 6px 4px -4px rgba(0,0,0,.2);
}
.container__data-label {
    display: flex;
    justify-content: center;
    font-weight: bold;
}
.container__data-parameters {
    display: block;
    margin-top: 20px;
    line-height: 250%;
}
</style>