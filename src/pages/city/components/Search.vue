<template>
  <div>
    <div class="container">
      <input type="text" v-model="keyword" placeholder="输入城市名或拼音"/>
    </div>
    <div class="search" ref="search" v-show="keyword">
      <ul>
        <li
          class="border-bottom"
          v-for="item of list"
          :key="item.id"
          @click="handleCityClick(item.name)"
        >{{item.name}}</li>
        <li class="border-bottom" v-show="hasNoData">
          没有找到匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let items in this.cities) {
          this.cities[items].forEach((value) => {
            if (value.spell.indexOf(this.keyword) === 0 || value.name.indexOf(this.keyword) === 0) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }
  },
  updated () {
    this.scroll = new Bscroll(this.$refs.search, {click: true, probeType: 1})
  }
}
</script>

<style lang="stylus" scoped>
  .container
    position: fixed
    top: .86rem
    width: 100%
    z-index: 99
    box-sizing: border-box
    height: .72rem
    padding: 0 .12rem
    background: #00bcd4

    input
      background: #fff
      border-radius: .04rem
      padding: 0 .1rem
      box-sizing: border-box
      width: 100%
      height: .6rem
    input:

    :-webkit-input-placeholder
      text-align: center

  .search
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    z-index: 1
    overflow: hidden
    background: #eee

    li
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>
<!--<template>-->
<!--  <div>-->
<!--    <div class="search">-->
<!--      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />-->
<!--    </div>-->
<!--    <div-->
<!--      class="search-content"-->
<!--      ref="search"-->
<!--      v-show="keyword"-->
<!--    >-->
<!--      <ul>-->
<!--        <li-->
<!--          class="search-item border-bottom"-->
<!--          v-for="item of list"-->
<!--          :key="item.id"-->
<!--          @click="handleCityClick(item.name)"-->
<!--        >-->
<!--          {{item.name}}-->
<!--        </li>-->
<!--        <li class="search-item border-bottom" v-show="hasNoData">-->
<!--          没有找到匹配数据-->
<!--        </li>-->
<!--      </ul>-->
<!--    </div>-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--import Bscroll from 'better-scroll'-->
<!--import {mapMutations} from 'vuex'-->

<!--export default {-->
<!--  name: 'CitySearch',-->
<!--  props: {-->
<!--    cities: Object-->
<!--  },-->
<!--  data () {-->
<!--    return {-->
<!--      keyword: '',-->
<!--      list: [],-->
<!--      timer: null-->
<!--    }-->
<!--  },-->
<!--  computed: {-->
<!--    hasNoData () {-->
<!--      return !this.list.length-->
<!--    }-->
<!--  },-->
<!--  watch: {-->
<!--    keyword () {-->
<!--      if (this.timer) {-->
<!--        clearTimeout(this.timer)-->
<!--      }-->
<!--      if (!this.keyword) {-->
<!--        this.list = []-->
<!--        return-->
<!--      }-->
<!--      this.timer = setTimeout(() => {-->
<!--        const result = []-->
<!--        for (let i in this.cities) {-->
<!--          this.cities[i].forEach((value) => {-->
<!--            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {-->
<!--              result.push(value)-->
<!--            }-->
<!--          })-->
<!--        }-->
<!--        this.list = result-->
<!--      }, 100)-->
<!--    }-->
<!--  },-->
<!--  methods: {-->
<!--    handleCityClick (city) {-->
<!--      this.changeCity(city)-->
<!--      this.$router.push('/')-->
<!--    },-->
<!--    ...mapMutations(['changeCity'])-->
<!--  },-->
<!--  mounted () {-->
<!--    this.scroll = new Bscroll(this.$refs.search)-->
<!--  }-->
<!--}-->
<!--</script>-->

<!--<style lang="stylus" scoped>-->
<!--  .search-->
<!--    height: .72rem-->
<!--    padding: 0 .1rem-->
<!--    background: #00bcd4-->
<!--    .search-input-->
<!--      box-sizing: border-box-->
<!--      width: 100%-->
<!--      height: .62rem-->
<!--      padding: 0 .1rem-->
<!--      line-height: .62rem-->
<!--      text-align: center-->
<!--      border-radius: .06rem-->
<!--      color: #666-->
<!--  .search-content-->
<!--    z-index: 1-->
<!--    overflow: hidden-->
<!--    position: absolute-->
<!--    top: 1.58rem-->
<!--    left: 0-->
<!--    right: 0-->
<!--    bottom: 0-->
<!--    background: #eee-->
<!--    .search-item-->
<!--      line-height: .62rem-->
<!--      padding-left: .2rem-->
<!--      background: #fff-->
<!--      color: #666-->
<!--</style>-->
