<template>
  <div class="banner">
    <swiper :options="swiperOption" class="swiper-container" v-if="show">
      <swiper-slide v-for="item of swiperList" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl" />
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    swiperList: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: 3000,
        loop: true,
        pagination: '.swiper-pagination',
        paginationClickable: true
      }
    }
  },
  computed: {
    show () {
      return this.swiperList.length
    }
  }
}
</script>

<style lang="stylus" scoped>
.banner
  height: 0
  padding-bottom: 31.25%
  background :#fff
  overflow: hidden
  .swiper-container >>> .swiper-pagination-bullet-active
    background :#fff
  .swiper-container
    width :100%
    height :0
    overflow :hidden
    padding-bottom: 31.25%
    .swiper-img
      width :100%

</style>
