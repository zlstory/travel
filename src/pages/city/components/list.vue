<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.currentCity}}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="area">
                    <div class="title border-topbottom">热门城市</div>
                    <div class="button-list">
                        <div class="button-wrapper" v-for="item of hot" :key="item.id" @click="handleCityClick(item.name)">
                            <div class="button">{{item.name}}</div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
                <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id" @click="handleCityClick(innerItem.name)">
                        {{innerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import BScroll from 'better-scroll'
    import { mapState,mapMutations } from 'vuex'
    export default {
        name: 'CityList',
        props: {
            cities: Object,
            hot: Array,
            letter: String
        },
        computed:{
            ...mapState({
                currentCity: 'city'
            })
        },
        mounted() {
            this.scroll = new BScroll(this.$refs.wrapper)
        },
        methods: {
            handleCityClick(city) {
                // this.$store.commit('changeCity', city)
                this.changeCity(city)
                this.$router.push('/')
            },
            ...mapMutations(['changeCity'])
        },
        watch: {
            letter() {
                if (this.letter) {
                    const element = this.$refs[this.letter][0]
                    this.scroll.scrollToElement(element, 400)
                }
            }
        }
    }
</script>

<style lang="stylus" scoped>
    @import '~styles/varibles.styl'
    .border-topbottom
        &:before
            border-color #ccc
        &:after
            border-color #ccc
    .border-bottom
        &:before
            border-color #ccc
    .list
        position absolute
        top 1.78rem
        right 0 
        bottom 0
        left 0
        overflow hidden
        .title
            line-height .54rem
            background #eeeeee
            padding-left .2rem
            font-size .26rem
            color #666666
        .button-list
            padding .1rem
            overflow hidden
            padding .1rem .6rem .1rem .1rem
            .button-wrapper
                width 33.33%
                float left
                .button
                    text-align center
                    margin .1rem
                    padding 0.1rem 0
                    border 0.02rem solid #eeeeee
                    border-radius .1rem
        .item-list
            .item
                line-height .76rem
                padding-left .2rem

</style>
