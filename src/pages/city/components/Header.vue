<template>
  <div class="header">
    <router-link tag="div" to="/" class="iconfont back-icon">&#xe624;</router-link>
    <p class="header-middle">城市选择</p>
  </div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>

<style lang="stylus" scoped>
  .header
    position: fixed
    z-index: 99
    width: 100%
    text-align : center
    line-height :.86rem
    background :#00bcd4
    color :#fff
    .back-icon
      position :absolute
      width :.64rem
      font-size : .4rem
    .header-middle
      font-size : .36rem
</style>
