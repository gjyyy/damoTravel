<template>
<div>
    <div class="banner" @click="handleBannerClick">
        <img :src="bannerImg" alt="" class="banner-img">
        <div class="banner-info">
            <p class="banner-title">{{this.sightName}}</p>
            <p class="banner-number">{{this.bannerImgs.length}}</p>
        </div>
        <CommonGallary :imgs="bannerImgs" v-show="showGallary" @close="handleGallaryClose"/>
    </div>
</div>

    
</template>
<script>
import CommonGallary from '@/common/gallary/gallary.vue'
export default {
    props:{
        bannerImg:String,
        bannerImgs:Array,
        sightName:String,
    },
    data (){
        return {
            showGallary:false
        }
    },
    methods:{
        handleBannerClick (){
            this.showGallary=true
        },
        handleGallaryClose (){
            this.showGallary=false
        }
    },
    components:{
        CommonGallary,

    }

}
</script>
<style lang="stylus" scoped>
.banner
    position relative
    overflow :hidden
    padding-bottom :55%
    height :0
    .banner-img
        width :100%
    .banner-info
        display flex
        position :absolute
        left :0
        right :0
        bottom :0
        line-height :.6rem
        .banner-title
            flex :1
            font-size :.32rem
            padding :0 .2rem
        .banner-number
            padding :0 .4rem
            line-height :.4rem
            margin-top :.14rem
            height :.32rem
            border-radius :.2rem
            background :rgba(0,0,0,.8)
            font-size :.24rem

</style>

