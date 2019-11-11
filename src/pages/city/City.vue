<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list
      :cities="cities"
      :hotCities="hotCities"
      :letter="letter"
      :arr="arr"
    ></city-list>
    <city-alphabet
      :cities="cities"
      @change="handleLetterChange"
      :letters="arr"
    ></city-alphabet>
  </div>
</template>
<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: '',
      arr: []
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.success)
        .catch((error) => console.log(error))
    },
    success (res) {
      if (res.data.ret) {
        var item
        let data = res.data.data
        this.cities = data.cities
        this.hotCities = data.hotCities
        for (item in this.cities) {
          this.arr.push(item)
        }
      }
    },
    handleLetterChange (key) {
      this.letter = key
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>
<style scoped lang="stylus">

</style>
