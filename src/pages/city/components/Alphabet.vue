<template>
    <ul class="list">
        <li class="item" v-for="item of letters" :key="item" :ref="item" @click="handleLetterClick" @touchstart="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchEnd">{{item}}</li>
    </ul>
</template>

<script>
    export default {
        name: "CityAlphabet",
        data() {
            return {
                touchStatus: false,
                startY: '',
                timer: null
            };
        },
        computed: {
            letters() {
                const letters = [];
                for (let i in this.cities) {
                    letters.push(i);
                }
                return letters;
            }
        },
        props: {
            cities: {}
        },
        updated() {
            this.startY = this.$refs['A'][0].offsetTop
        },
        methods: {
            handleLetterClick(e) {
                this.$emit("change", e.target.innerText);
            },
            handleTouchStart() {
                this.touchStatus = true;
            },
            handleTouchMove(e) {
                if (this.touchStatus) {
                    if (this.timer) {
                        clearTimeout(this.timer)
                    }
                    this.timer = setTimeout(() => {
                        const touchY = e.touches[0].clientY - 79
                        const index = Math.floor((touchY - this.startY) / 20)
                        if (index >= 0 && index < this.letters.length) {
                            this.$emit('change', this.letters[index])
                        }
                    }, 16)
                }
            },
            handleTouchEnd() {
                this.touchStatus = false;
            }
        }
    };
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';

.list {
    top: 1.58rem;
    bottom: 0;
    right: 0;
    width: 0.4rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
    position: absolute;

    .item {
        line-height: 0.4rem;
        text-align: center;
        color: $bgColor;
    }
}
</style>
