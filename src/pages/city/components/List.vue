
<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热点城市</div>
        <div class="button-list">
          <div
            class="button-wrapper"
            v-for="item in hotCities"
            :key="item.id"
            @click="handleCityClick(item.name)"
          >
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div
        class="area"
        v-for="(item, key) in cities"
        :key="key.toString()"
        ref="key"
      >
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div
            class="item border-bottom"
            v-for="innerItem in item"
            :key="innerItem.id"
            @click="handleCityClick(innerItem.name)"
          >
            {{innerItem.name}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    cities: {
      type: Object,
      default () {
        return {}
      }
    },
    hotCities: {
      type: Array,
      default () {
        return []
      }
    },
    letter: {
      type: String
    },
    arr: {
      type: Array
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper, {
      click: true
    })
  },
  methods: {
    handleCityClick (name) {
      this.changeCity(name)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  computed: {
    len () {
      let len = this.arr.length
      return len
    },
    ...mapState({
      currentCity: 'city'
    })
  },
  watch: {
    letter () {
      if (this.letter) {
        let num
        for (let i = 0; i < this.len; i++) {
          if (this.letter === this.arr[i]) {
            num = i
            break
          }
        }
        const element = this.$refs.key[num]
        this.scroll.scrollToElement(element)
      }
    }
  }
}
</script>
<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .border-topbottom
    &:before
      border-color: #ccc
    &:after
      border-color: #ccc
  .border-bottom
    &:before
      border-color: #ccc
    &:after
      border-color: #ccc
  .list
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    .title
      line-height: .54rem
      background: #eeeeee
      padding-left: .2rem
      color: #666
      font-size: .26rem
    .button-list
      overflow: hidden
      padding: .1rem .6rem .1rem .1rem
      .button-wrapper
        float: left
        width: 33.33%
      .button
        margin: .1rem
        padding: .1rem 0
        text-align: center
        border: .02rem solid #ccc
        border-radius: .06rem
    .item-list
      .item
        line-height: .46rem
        padding: .2rem
</style>
