<template>
  <div>
    <detail-banner
      :imgs="imgs"
      :bannerImg="bannerImg"
      :sightName="sightName"
      :number="number"
    ></detail-banner>
    <detail-header></detail-header>
    <detail-list :list="categoryList"></detail-list>
    <div class="content"></div>
  </div>
</template>
<script>
import axios from 'axios'
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
export default {
  name: 'Detail',
  components: {
    DetailBanner,
    DetailHeader,
    DetailList
  },
  data () {
    return {
      categoryList: [],
      imgs: [],
      bannerImg: '',
      sightName: '',
      number: null,
      lastId: null,
      id: null
    }
  },
  mounted () {
    this.lastId = this.id
    this.getData()
  },
  methods: {
    getData () {
      this.id = this.$route.params.id
      axios.get('/api/detail.json?id=' + this.id)
        .then(this.success)
        .catch((error) => console.log(error))
    },
    success (res) {
      if (res.data.ret) {
        let data = res.data.data
        this.categoryList = data.categoryList
        this.imgs = data.imgs
        this.bannerImg = data.bannerImg
        this.sightName = data.sightName
        this.number = data.number
      } else {
        console.log('数据获取异常')
      }
    }
  },
  activated () {
    console.log(this.lastId, this.id)
    if (this.lastId !== this.id) {
      this.lastId = this.id
      this.getData()
    }
  }
}
</script>
<style scoped lang="stylus">
  .content
    height: 8rem
</style>
