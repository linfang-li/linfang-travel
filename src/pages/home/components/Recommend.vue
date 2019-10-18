<template>
  <div class="container">
    <div class="recommend">热销推荐</div>
    <router-link tag="div" class="content border-bottom" v-for="item of recommendList" :key="item.id" :to="'/detail/' + item.id">
      <div class="img-container"><img class="img" :src="item.imgUrl"/></div>
      <div class="text-container">
        <p class="text-title">{{item.title}}</p>
        <p>{{item.desc}}</p>
        <p class="text-price">58起</p>
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'HomeRecommend',
  props: {
    recommendList: Array
  }
}
</script>

<style lang="stylus" scoped>
  .container
    height: 12.86rem
    box-sizing: border-box

    .recommend
      line-height: .86rem
      padding: 0 .3rem
      background: #eee
      font-size: .36rem

    .content
      display: flex
      padding: .3rem

      .img-container
        width: 1.8rem

        .img
          width: 100%

      .text-container
        margin-left: .3rem
        display: flex
        flex-direction :column
        justify-content: space-between

        .text-title
          font-size: .36rem
        .text-price
          font-size: .32rem
          color: #ffc92a

</style>
