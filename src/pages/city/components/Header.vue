<template>
    <div class="header">
        城市选择
        <router-link to="/"><!-- 回到首页 根路径下 -->
            <div class="iconfont header-back">&#xe624;</div>
        </router-link>
    </div>
</template>

<script>
    export default {
        name: 'CityHeader'
    }
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
    .header
        height $headerHeight
        line-height $headerHeight
        text-align center
        color #ffffff
        background $bgColor
        font-size .32rem
        position relative
        .header-back 
            width .64rem
            text-align center
            font-style .4rem
            position absolute
            top 0
            left 0
            color #fff
</style>
