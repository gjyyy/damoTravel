<template>
<div class="wrapper">
    <swiper :options="swiperOption" v-if="list.length">
        <swiper-slide v-for="index of list" :key="index.id">
            <img class="swiper-img" :src="index.imgUrl"/>
        </swiper-slide>
    
        <!-- Optional controls -->
        <div class="swiper-pagination"  slot="pagination"></div>
        
    </swiper>
</div>
    
</template>
<script>
export default {
    props:{
        list:Array
    },
    data(){
        return {
            swiperOption:{
                pagination: '.swiper-pagination',
                loop: true
            }
        }
    }
}
</script>

<style lang="stylus" scoped>
.wrapper >>> .swiper-pagination-bullet-active
    background :#fff
@import "swiper/dist/css/swiper.css"
.wrapper
    overflow :hidden
    width :100%
    height :0
    padding-bottom :31.25%
</style>
