<template>
<!--  <div class="container">-->
<!--    <div  class="icons" v-for="item of iconList" :key="item.id">-->
<!--      <div class="img-container">-->
<!--        <img class="img" :src="item.imgUrl" >-->
<!--      </div>-->
<!--      <p class="content">{{item.desc}}</p>-->
<!--    </div>-->
<!--  </div>-->
  <div class="container">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page, index) of pages" :key="index">
        <div  class="icons" v-for="item of page" :key="item.id">
          <div class="img-container">
            <img class="img" :src="item.imgUrl" >
          </div>
          <p class="content">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcon',
  props: {
    iconList: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.iconList.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
  /*.container*/
  /*  height: 0*/
  /*  padding-bottom: 50%*/
  /*  overflow :hidden*/
  /*  .icons*/
  /*    width: 25%*/
  /*    height: 0*/
  /*    overflow :hidden*/
  /*    padding-bottom: 25%*/
  /*    display: inline-block*/
  /*    .img-container*/
  /*      padding: .2rem .4rem*/
  /*      .img*/
  /*        width: 100%*/
  /*    .content*/
  /*      text-align: center*/
  .container >>> .swiper-container
    height: 0
    padding-bottom: 50%
  .icons
    width: 25%
    height: 0
    overflow :hidden
    padding-bottom: 22%
    display: inline-block
    .img-container
      padding: .2rem .5rem
      .img
        width: 100%
    .content
      text-align: center
</style>
