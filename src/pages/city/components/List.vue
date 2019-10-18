<template>
  <div class="wrapper" ref="wrapper">
    <div>
      <div class="recommend">当前城市</div>
      <div class="content">
        <button>{{this.$store.state.city}}</button>
      </div>
      <div class="recommend">热门城市</div>
      <div class="content">
        <button
          v-for="item of hotCities"
          :key="item.id"
          @click="handleCityClick(item.name)"
        >{{item.name}}</button>
      </div>
      <div v-for="(item,key) of cities" :key="key" :ref="key">
        <div class="recommend">{{key}}</div>
        <div
          class="list border-bottom"
          v-for="inneritem of item"
          :key="inneritem.id"
          @click="handleCityClick(inneritem.name)"
        >{{inneritem.name}}</div>
      </div>
    </div>
    <transition name="fade">
      <div class="toast" v-show="showToast">
        <span class="letter">{{this.letter}}</span>
      </div>
    </transition>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'

export default {
  name: 'CityList',
  props: {
    hotCities: Array,
    cities: Object,
    letter: String
  },
  data () {
    return {
      showToast: false
    }
  },
  methods: {
    changeToast () {
      this.showToast = true
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        this.showToast = false
      }, 200)
    },
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }
  },
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element, 10)
        this.changeToast()
      }
    }
  },
  updated () {
    this.scroll = new Bscroll(this.$refs.wrapper, {click: true, probeType: 1})
  }
}

</script>

<style lang="stylus" scoped>
  .wrapper
    overflow: hidden
    position: absolute
    top: 1.58rem
    bottom: 0

    .recommend
      width: 100%
      line-height: .72rem
      padding: 0 .3rem
      background: #eee

    .list
      line-height: .72rem
      padding: 0 .3rem
      background: #fff

    .content
      padding-bottom: .15rem
      background: #fff

      button
        box-sizing: border-box
        width: 2rem
        margin: .15rem 0 0 .15rem
        padding: .06rem
        background: #fff
        border: 1px solid #ddd
        border-radius: .04rem

    .toast
      position fixed
      top 50%
      left 50%
      transform translate(-50%, -50%)
      z-index 10
      width 50px
      height 50px
      background #ed4e5e
      border-radius 50%
      text-align center
      transition all 0.5s

      &.fade-enter
        opacity 0

      &.fade-leave, &.fade-enter-active
        opacity 1

      &.fade-leave-active
        opacity 0

      .letter
        line-height 50px
        font-size 16px
        font-weight 700
        color #eee
</style>
