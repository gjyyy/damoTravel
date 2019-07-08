<template>
<div>
    <CityHeader/>
    <Search :cities="cities"/>
    <CityList :cities="cities" :hotCities="hotCities" :letter="letter"/>
    <Alphabet :cities="cities" @change="handleLetterChange" />
</div>
    
</template>

<script>
import axios from 'axios'
import CityHeader from '@/components/cityHeader.vue'
import Search from '@/components/search.vue'
import CityList from '@/components/cityList.vue'
import Alphabet from '@/components/Alphabet.vue'
export default {
    components:{
        CityHeader,
        Search,
        CityList,
        Alphabet,
    },
    data(){
        return {
            cities:{},
            hotCities:[],
            letter:''
        }
    },
    methods:{
        getCityInfo(){
            axios.get('/static/mock/city.json')//get到的是一个promise
                .then(this.getCityInfoSucc)
        },
        getCityInfoSucc(res){
            console.log(res)
            res=res.data
            if(res.ret&&res.data){
                const data=res.data
                this.cities=data.cities
                this.hotCities=data.hotCities
            }
        },
        handleLetterChange(letter){
            this.letter=letter
        }
    },
    mounted(){
        this.getCityInfo()
    }
}
</script>
<style>

</style>

