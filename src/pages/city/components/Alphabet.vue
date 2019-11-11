<template>
  <ul class="list">
    <li class="item"
      v-for="item in letters"
      :key="item.toString()"
      :ref="item"
      @click="handleLetterClick(item)"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      {{item}}
    </li>
  </ul>
</template>
<script>
export default {
  name: 'CityAlphabet',
  data () {
    return {
      touchStatus: false,
      starY: 0,
      timer: null
    }
  },
  updated () {
    this.starY = this.$refs['A'][0].offsetTop
  },
  props: {
    cities: {
      type: Object,
      default () {
        return {}
      }
    },
    letters: {
      type: Array
    }
  },
  methods: {
    handleLetterClick (key) {
      this.$emit('change', key)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.starY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>
<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .list
    display: flex
    flex-direction: column
    justify-content: center
    position: absolute
    top: 1.58rem
    right: 0
    bottom: 0
    width: .4rem
    .item
      line-height: .4rem
      text-align: center
      color: $bgColor
</style>
