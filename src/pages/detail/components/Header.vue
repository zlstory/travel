<template>
    <div>
        <router-link tag="div" to='/' class="header-abs" v-show="showAbs">
            <div class="iconfont back-icon header-abs-back">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
            <router-link to="/">
                <!-- 回到首页 根路径下 -->
                <div class="iconfont header-fixed-back">&#xe624;</div>
            </router-link>
            景点详情
        </div>
    </div>
</template>

<script>
    export default {
        name: 'DetailHeader',
        data() {
            return {
                showAbs: true,
                opacityStyle: {
                    opacity:0
                }
            }
        },
        methods: {
            handleScroll() {
                const top = document.documentElement.scrollTop
                if(top > 60 ){
                    console.log(1)
                    let opacity = top / 140
                    opacity = opacity > 1 ? 1 : opacity
                    this.opacityStyle = {opacity}
                    this.showAbs = false
                }else{
                    this.showAbs = true
                }
            }
        },
        mounted() {
            window.addEventListener('scroll', this.handleScroll)
        },
        unmounted() {
            window.removeEventListener('scroll', this.handleScroll)
        }
    }
</script>

<style lang="stylus" scope>
    @import '~styles/varibles.styl';    
    .header-abs
        position absolute
        left .2rem
        top .2rem
        width .8rem
        height .8rem
        line-height .8rem
        border-radius .4rem
        text-align center
        background rgba(0,0,0,.8)
        .header-abs-back
            color #ffffff
            font-size .4rem
    .header-fixed
        height $headerHeight
        line-height $headerHeight
        text-align center
        color #ffffff
        background $bgColor
        z-index 2
        font-size .32rem
        position fixed
        left 0
        right 0 
        top 0
        .header-fixed-back 
            width .64rem
            text-align center
            font-style .4rem
            position absolute
            top 0
            left 0
            color #fff

</style>
