<template>
<div class="alphabet">
    <ul class="list">
        <li class="item" v-for="item of letters" 
        :key="item" 
        :ref="item"
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        @click="handleLetterClick">{{item}}</li>      
    </ul>

</div>
</template>
<script>
import { clearTimeout, setTimeout } from 'timers';
export default {
    props:{
        cities:Object
    },
    computed:{
        //获取cities数组
        letters (){
            const letters=[]
            for(let i in this.cities){
                letters.push(i)
            }
            return letters
        }
    },
    data(){
        return {
            touchStatus:false,
            timer:null
        }
    },
    methods:{
        handleLetterClick (e){
            this.$emit('change',e.target.innerText)
        },
        handleTouchStart (){
            this.touchStatus=true
        },
        handleTouchMove (e){
            if(this.touchStatus){
                if(this.timer){
                    clearTimeout(this.timer)
                }
                this.timer=setTimeout(()=>{
                    //通过offsetTop获得A元素距离顶部的高度
                    const startY=this.$refs['A'][0].offsetTop
                    //获取触点到顶部的高度
                    const touchY=e.touches[0].clientY-79
                    //获取字母下标，每个字母的高度是20,并向下取整
                    const index=Math.floor((touchY-startY)/20)
                    if(index >= 0 &&index<this.letters.length){
                        this.$emit('change',this.letters[index])
                    }
                },16)
            }
        },
        handleTouchEnd (){
            this.touchStatus=false
        },
    }
}
</script>
<style lang="stylus" scoped>
@import "../assets/styles/varibles.styl";
.list 
    display :flex
    flex-direction :column
    justify-content :center
    position :absolute
    right :0
    bottom :0
    top :1.58rem 
    width :.4rem
    .item
        text-align :center
        line-height :.44rem
        color :$bgColor

</style>
