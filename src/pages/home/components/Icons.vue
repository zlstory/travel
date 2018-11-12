<template>
    <div class="icons">
        <swiper :options="swiperOption1">
            <swiper-slide v-for="(page,index) of pages" :key="index">
                <div class="icon" v-for="item of page" :key="item.id">
                    <div class="icon-img">
                        <img :src="item.imgUrl" alt="">
                    </div>
                    <p class="icon-desc">{{item.desc}}</p>
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>

<script>
    export default {
        name: "HomeIcons",
        props: {
            list: Array
        },
        data() {
            return {
                swiperOption1: {
                    autoPlay: false
                }
            }
        },
        computed: {
            pages() {
                const pages = []
                this.list.forEach((item, index) => {
                    const page = Math.floor(index / 8) //看数据到底展示在哪一页,从0开始
                    if (!pages[page]) { //如果不存在(一开始的情况)
                        pages[page] = []
                    }
                    pages[page].push(item) //将item放入pages中
                })
                return pages
            }
        }
    }
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
@import '~styles/mixins.styl'
    .icons >>> .swiper-container
        width 100%
        height 0
        padding-bottom 50%
    .icons
        margin-top 0.1rem
        .icon
            width 25%
            height 0
            padding-bottom 25%
            float left
            overflow hidden
            position relative
            .icon-img
                position absolute
                top 0
                left 0
                right 0
                bottom .44rem
                box-sizing border-box
                padding 0.1rem
                img
                    height 100%
                    display block
                    margin 0 auto
            .icon-desc
                position absolute
                bottom 0
                left 0
                right 0
                line-height .44rem
                height .44rem
                color $darkTextColor
                text-align center
                ellipsis()

</style>

