<template>
    <div>
        <div class="banner" @click="handleBannerClick">
            <img class="banner-img" :src="bannerImg" alt="">
            <div class="banner-info">
                <div class="banner-title">{{this.sightName}}</div>
                <div class="banner-number"> <span class="iconfont banner-icon">&#xe60e;</span>{{this.bannerImgs.length}}</div>
            </div>
        </div>
        <FadeAnimation>
            <common-gallary :imgs="bannerImgs" v-show="showGallaey" @close="handleGallaryClose"></common-gallary>
        </FadeAnimation>
    </div>
</template>

<script>
    import CommonGallary from 'common/gallary/Gallary'
    import FadeAnimation from 'common/fade/FadeAnimation'
    export default {
        name: 'DetailBanner',
        props: {
            sightName: String,
            bannerImg: String,
            bannerImgs: Array
        },
        data() {
            return {
                showGallaey: false,
            }
        },
        components: {
            CommonGallary,
            FadeAnimation
        },
        methods: {
            handleBannerClick() {
                this.showGallaey = true
            },
            handleGallaryClose() {
                this.showGallaey = false
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .banner
        position relative
        overflow hidden
        height 0
        padding-bottom 55%
        .banner-img
            width 100%
        .banner-info
            display flex
            position absolute
            left 0
            right 0
            bottom 0
            line-height .6rem
            color #fff
            background-image linear-gradient(top,rgba(0,0,0,0),rgba(0,0,0,.8))
            .banner-title
                flex 1
                font-size .32rem
                padding-left .2rem
            .banner-number
                margin-top .14rem
                padding 0 .4rem
                line-height .32rem
                height .32rem
                font-size .24rem
                border-radius .2rem
                background rgba(0,0,0,.8)
                .banner-icon
                    font-size .24rem
                    
</style>
