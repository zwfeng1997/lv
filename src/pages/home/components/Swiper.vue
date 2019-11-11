<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
      <!-- slides -->
      <swiper-slide
        v-for="item in swiperList"
        :key="item.id"
      >
        <img class="swiper-img" :src=item.imgUrl />
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>
<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        autoplay: {
          delay: 1500,
          stopOnLastSlide: false,
          disableOnInteraction: true
        },
        loop: true
      }
    }
  },
  props: {
    swiperList: {
      type: Array,
      default () {
        return []
      }
    }
  }
}
</script>
<style lang="stylus" scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #fff
  .wrapper
    width: 100%
    height: 0
    padding-bottom: 30.46%
    background: #eee
    .swiper-img
      width: 100%
</style>
