<template>
    <div>
        <Detail-banner :sightName="sightName" 
                       :bannerImg="bannerImg"
                       :bannerImgs="gallaryImgs"></Detail-banner>
        <Detail-header></Detail-header>
        <div class="content">
            <Detail-list :list="list"></Detail-list>
        </div>
    </div>
</template>

<script>
    import DetailBanner from './components/Banner'
    import DetailHeader from './components/Header'
    import DetailList from './components/List'
    import axios from 'axios'
    export default {
        name: 'Detail',
        components: {
            DetailBanner,
            DetailHeader,
            DetailList
        },
        data() {
            return {
                sightName:'',
                bannerImg:'',
                gallaryImgs:[],
                list: []
            }
        },
        methods: {
            getDetailInfo() {
                axios.get('/api/detail.json', {
                        params: {
                            id: this.$route.params.id
                        }
                    }).then(this.handleGetDataSucc)
                },
                handleGetDataSucc(res){
                    res = res.data
                    if(res.ret && res.data){
                        const data = res.data
                        this.sightName = data.sightName
                        this.bannerImg = data.bannerImg
                        this.gallaryImgs = data.gallaryImgs
                        this.list = data.categoryList
                    }

                }
            },
            mounted() {
                this.getDetailInfo()
            }
        }
</script>
<style lang="stylus" scoped>
    .content
        height 50rem
</style>
