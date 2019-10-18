<template>
  <div class="container">
    <div class="recommend">周末去哪儿</div>
    <div class="content" v-for="item of weekendList" :key="item.id">
      <div class="img-container"><img :src="item.imgUrl"/></div>
      <div class="text-container">
        <p class="text-title">{{item.title}}</p>
        <p>{{item.desc}}</p>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'HomeWeekend',
  props: {
    weekendList: Array
  }
}
</script>

<style lang="stylus" scoped>
  .container
    margin-top: .2rem

    .recommend
      line-height: .86rem
      padding: 0 .3rem
      background: #eee
      font-size: .36rem
    .content
      display: flex
      flex-direction :column

      .img-container
        img
          width: 100%
      .text-container
        padding: .3rem

        .text-title
          font-size: .36rem
          margin-bottom: .2rem

</style>
