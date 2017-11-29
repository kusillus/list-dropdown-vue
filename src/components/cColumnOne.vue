<template>
  <div>
    <button @click="getDataJson()">ClickMe</button>
    <div class="columnOne">
      <div class="header">header</div>
      <div class="content">
        aqui va tu componente
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
      console.log(value)
      this.titleActive = value
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
  .content{
    // background: green;
  }
</style>
