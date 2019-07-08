<template>
    <div>
        
        <DetailHeader/>
        <DetailBanner :sightName="sightName" :bannerImg="bannerImg" :bannerImgs="gallaryImgs" />
        <div class="content">
            <DetailList :list="list"/>
        </div>

    </div>
</template>
<script>
import DetailList from '@/components/detailList.vue'
import DetailHeader from '@/components/detailHeader.vue'
import DetailBanner from '@/components/detailBanner.vue'
import axios from 'axios'
export default {
    name:'Detail',
    components:{
        DetailList,
        DetailHeader,
        DetailBanner,
    },
    data (){
        return {
            sightName:'',
            bannerImg:'',
            gallaryImgs:[],
            list:[],
        }
    },
    methods :{
        getDetailInfo(){
            axios.get('/static/mock/detail.json',{
                params:{
                    id:this.$route.params.id
                }
            }).then(this.getDetailInfoSucc)
        },
        getDetailInfoSucc(res){
            res=res.data
            if(res.ret&&res.data){
                const data=res.data
                this.sightName=data.sightName
                this.bannerImg=data.bannerImg
                this.gallaryImgs=data.gallaryImgs
                this.list=data.categoryList
            }
        }
    },
    mounted(){
        this.getDetailInfo()
    }

}
</script>
<style lang="stylus" scoped>

</style>
