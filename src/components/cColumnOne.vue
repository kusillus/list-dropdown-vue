<template>
  <div>
    <button class="btn" @click="getDataJson()">Load data</button>
    <div class="columnOne">
      <div class="content">
        <list-data
          :model="dataResponse"
          :active="titleActive"
          v-on:activeGuideline="setActiveGuideline">
        </list-data>
      </div>
    </div>
  </div>
</template>

<script>
import listData from './cTree'
import axios from 'axios'
export default {
  data () {
    return {
      dataJson: '../public/dummies/data.json',
      dataResponse: [],
      titleActive: ''
    }
  },
  computed: {
    dateNow: function () {
      let date = new Date()
      let day = date.getDate()
      let month = date.getMonth() + 1
      let year = date.getFullYear()
      let fullDate = year+'-'+month+'-'+day
      return fullDate
    }
  },
  methods: {
    getDataJson: function () {
      let vm = this
      axios.get(vm.dataJson)
      .then( function ( response ) {
        console.log(response.data.feed_list)
        let res = response.data
        vm.dataResponse = res.feed_list
      })
    },
    setActiveGuideline: function (value) {
      let params = {
        'idFeed': value.idFeed,
        'idGupi': value.idGupi,
        'blocksId': value.blocks_list_id,
        'date': this.dateNow
      }
      console.log(params)
      this.titleActive = value.guideline_name
    }
  },
  components: {
    'list-data': listData
  }

}
</script>

<style lang="scss">
  .columnOne{
    width: 20rem;
    // background-color: red;
    margin: 0 auto;
  }
  .header{
    width: 100%;
    // background-color: orange;
  }
  .btn{
    cursor: pointer;
    border: none;
    padding: .5rem 1rem;
    background: #00A3FF;
    border-radius: 0.1rem;
    color: white;
    font-weight: bold;
    outline: none;
    &:hover{
      background: #0298ec;
    }
  }
</style>
