<template>
    <div class="header">
      <div class="iconfont back-icon">&#xe624;</div>
      <div class="header-middle">
        <span class="iconfont">&#xe632;</span>输入城市/景点/游玩主题
      </div>
      <router-link tag="div" to="/City" class="header-right">
        {{this.$store.state.city}}<span class="iconfont arrow-icon">&#xe64a;</span>
      </router-link>
    </div>
</template>

<script>
export default {
  name: 'HomeHeader'
}
</script>

<style lang="stylus" scoped>
.header
  display :flex
  line-height :.86rem
  background :#00bcd4
  color :#fff
  .back-icon
    width :.64rem
    text-align : center
    font-size : .4rem
  .header-middle
    flex :1
    background :#fff
    color :#cacaca
    border-radius :.1rem
    margin :.12rem
    padding-left :.2rem
    line-height :.62rem
  .header-right
    text-align: center
    .arrow-icon
      font-size: .24rem
      padding: 0 .15rem 0 .05rem

</style>
