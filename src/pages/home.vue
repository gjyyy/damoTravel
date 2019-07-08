<template>
<div class="home">
    <Homeheader/>
    <Homeswiper :list='swiperList'/>
    <Icon :list='iconsList'/>
    <Recommend :list='recommendList'/>
    <Weekend :list='weekendList'/>
</div>    
</template>

<script>
import Homeheader from "../components/homeHeader.vue"
import Homeswiper from "../components/swiper.vue"
import Icon from "../components/icon.vue"
import Recommend from "../components/recommend.vue"
import Weekend from "../components/weekend.vue"
import axios from "axios"
import { mapState } from 'vuex'
export default {
    components:{
        Homeheader,
        Homeswiper,
        Icon,
        Recommend,
        Weekend,
    },
    data(){
        return {
            lastCity:'',
            swiperList:[],
            iconsList:[],
            recommendList:[],
            weekendList:[],
        }
    },
    mounted () {
        this.getHomeInfo()
        this.lastCity=this.city
    },
    computed:{
        ...mapState(['city'])
    },
    methods :{
        getHomeInfo () {
            axios.get('/static/mock/index.json?city='+this.city)
                .then(this.getHomeInfoSucc)
        },
        getHomeInfoSucc(res){
            res=res.data
            if(res.ret && res.data){
                this.swiperList=res.data.swiperList
                this.iconsList=res.data.iconsList
                this.recommendList=res.data.recommendList
                this.weekendList=res.data.weekendList
            }
        }
    },
    activated(){
        if (this.lastCity !== this.city) {
            this.lastCity=this.city
            this.getHomeInfo()
        }
    }
}
</script>

<style lang="stylus" scoped>

</style>
