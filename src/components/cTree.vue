<template>
  <!-- <li :class="{active: isActive(model.idChild)}"> -->
    <!-- <div :class="{bold: isFolder}" @click="toggle(model.idChild)" >
      <div v-if="isFolder" class="folder">
        <div v-if="open">
          <svg xmlns="http://www.w3.org/2000/svg" style="fill:#4C4C4C;" width="25" height="25" viewBox="0 0 24 24"><path d="M19,20H4C2.89,20 2,19.1 2,18V6C2,4.89 2.89,4 4,4H10L12,6H19A2,2 0 0,1 21,8H21L4,8V18L6.14,10H23.21L20.93,18.5C20.7,19.37 19.92,20 19,20Z" /></svg>
        </div>
        <div v-else>
          <svg xmlns="http://www.w3.org/2000/svg" style="fill:#4C4C4C;" width="25" height="25" viewBox="0 0 24 24"><path d="M10,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V8C22,6.89 21.1,6 20,6H12L10,4Z" /></svg>
        </div>
        <div class="arrow-folder" v-if="open">
          <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="24" height="24" viewBox="0 0 24 24"><path d="M7,15L12,10L17,15H7Z" /></svg>
        </div>
        <div class="arrow-folder" v-else>
          <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="24" height="24" viewBox="0 0 24 24"><path d="M7,10L12,15L17,10H7Z" /></svg>
        </div>
      </div>
      <span>{{model.name }}</span>
      <span v-if="!isFolder">
        ({{model.count}})
      </span>
    </div> -->
    <div>
      <div class="feed-wrapper" v-for="item in model" :key="item.feed_name">
        <div class="feed-item">
          {{item.feed_name}}
          <div class="btns">
            <i v-if="item.isFolder" @click="showHideGuideline(item, true)">
              <svg style="width:20px;height:20px" viewBox="0 0 24 24">
                <path fill="#000000" d="M22,4A2,2 0 0,1 24,6V16A2,2 0 0,1 22,18H6A2,2 0 0,1 4,16V4A2,2 0 0,1 6,2H12L14,4H22M2,6V20H20V22H2A2,2 0 0,1 0,20V11H0V6H2M6,6V16H22V6H6Z" />
              </svg>
            </i>
            <i v-else @click="showHideGuideline(item, false)">
              <svg style="width:20px;height:20px" viewBox="0 0 24 24">
                <path fill="#000000" d="M20,18H4V8H20M20,6H12L10,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V8C22,6.89 21.1,6 20,6Z" />
              </svg>
            </i>
            <i class="icon-guide">
                <svg style="width:24px;height:24px" viewBox="0 0 24 24">
                  <path fill="#000000" d="M7,10L12,15L17,10H7Z" />
                </svg>
              </i>
          </div>
        </div>
        <ul class="guidelines-list">
          <li class="guidelines-wrapper" v-for="el in item.guidelines_list" :key="el.guideline_name">
            <div class="guidelines-item">
              <span :class="{strongGruideline: isSelect(el.guideline_name)}" @click="setActiveGuideline(el.guideline_name)">{{el.guideline_name}}</span>
              <i class="icon-guide" :class="{openMopdal: !el.isFolder}" @click="el.isFolder=!el.isFolder">
                <svg style="width:24px;height:24px" viewBox="0 0 24 24">
                  <path fill="#000000" d="M7,10L12,15L17,10H7Z" />
                </svg>
              </i>
            </div>
            <transition name="changeHeight" mode="out-in">
              <div style="padding-left: 2rem;" v-if="el.isFolder">
                <div class="block" v-for="block in el.blocks_list" :key="block.block_name">{{block.block_name}}</div>
              </div>
            </transition>
          </li>
        </ul>
      </div>

      <!-- <ul v-show="open" v-if="isFolder" class="tree">
        <item class="child"
          v-for="(model,key) in model.children"
          :model="model" :key='key.id'
          :active="active">
        </item>
      </ul> -->
    </div>
    <!-- <span v-else class="file">
      <div v-if="model.state === 0">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 21.98 30.49" width="20px" height="20px"><title>Asset 22ldpi</title><g id="Layer_2" data-name="Layer 2"><g id="Layer_1-2" data-name="Layer 1"><path d="M15.82,0H2A2,2,0,0,0,0,2v26.4a2,2,0,0,0,2,2H19.93a2,2,0,0,0,2-2V6.16Z" style="fill:#ffb300"/><path d="M15.8,0h-.51V4.62a2.55,2.55,0,0,0,2.55,2.55H22v-1Z" style="fill:#ffa000"/><path d="M7.31,21.87H5.68a1.26,1.26,0,0,1-1.26-1.26V19a1.26,1.26,0,0,1,1.26-1.26c2.09.11,2.91,1.19,2.88,2.88A1.26,1.26,0,0,1,7.31,21.87Z" style="fill:#fff"/><path d="M11.52,21.95a1.25,1.25,0,0,1-1.24-1.13c-.31-3.08-1.91-4.68-5.06-5a1.25,1.25,0,1,1,.28-2.48c4.33.5,6.84,3,7.26,7.28a1.25,1.25,0,0,1-1.12,1.37Z" style="fill:#fff"/><path d="M16.72,22.06a1.36,1.36,0,0,1-1.35-1.23c-.61-6.18-4-9.53-10.27-10.25a1.36,1.36,0,1,1,.31-2.71c7.55.87,11.93,5.25,12.67,12.69a1.36,1.36,0,0,1-1.22,1.49Z" style="fill:#fff"/></g></g></svg>
      </div>
      <div v-else-if="model.state === 1">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 21.98 30.49" width="20px" height="20px"><g id="Layer_2" data-name="Layer 2"><g id="Layer_1-2" data-name="Layer 1"><path d="M15.82,0H2A2,2,0,0,0,0,2v26.4a2,2,0,0,0,2,2H19.93a2,2,0,0,0,2-2V6.16Z" style="fill:#4caf50"/><path d="M15.8,0h-.51V4.62a2.55,2.55,0,0,0,2.55,2.55H22v-1Z" style="fill:#388e3c"/><path d="M7.31,21.87H5.68a1.26,1.26,0,0,1-1.26-1.26V19a1.26,1.26,0,0,1,1.26-1.26c2.09.11,2.91,1.19,2.88,2.88A1.26,1.26,0,0,1,7.31,21.87Z" style="fill:#fff"/><path d="M11.52,21.95a1.25,1.25,0,0,1-1.24-1.13c-.31-3.08-1.91-4.68-5.06-5a1.25,1.25,0,1,1,.28-2.48c4.33.5,6.84,3,7.26,7.28a1.25,1.25,0,0,1-1.12,1.37Z" style="fill:#fff"/><path d="M16.72,22.06a1.36,1.36,0,0,1-1.35-1.23c-.61-6.18-4-9.53-10.27-10.25a1.36,1.36,0,1,1,.31-2.71c7.55.87,11.93,5.25,12.67,12.69a1.36,1.36,0,0,1-1.22,1.49Z" style="fill:#fff"/></g></g></svg>
      </div>
      <div v-else-if="model.state === 2">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 21.98 30.49" width="20px" height="20px"><g id="Layer_2" data-name="Layer 2"><g id="Layer_1-2" data-name="Layer 1"><path d="M15.82,0H2A2,2,0,0,0,0,2v26.4a2,2,0,0,0,2,2H19.93a2,2,0,0,0,2-2V6.16Z" style="fill:#f44336"/><path d="M15.8,0h-.51V4.62a2.55,2.55,0,0,0,2.55,2.55H22v-1Z" style="fill:#d32f2f"/><path d="M7.31,21.87H5.68a1.26,1.26,0,0,1-1.26-1.26V19a1.26,1.26,0,0,1,1.26-1.26c2.09.11,2.91,1.19,2.88,2.88A1.26,1.26,0,0,1,7.31,21.87Z" style="fill:#fff"/><path d="M11.52,21.95a1.25,1.25,0,0,1-1.24-1.13c-.31-3.08-1.91-4.68-5.06-5a1.25,1.25,0,1,1,.28-2.48c4.33.5,6.84,3,7.26,7.28a1.25,1.25,0,0,1-1.12,1.37Z" style="fill:#fff"/><path d="M16.72,22.06a1.36,1.36,0,0,1-1.35-1.23c-.61-6.18-4-9.53-10.27-10.25a1.36,1.36,0,1,1,.31-2.71c7.55.87,11.93,5.25,12.67,12.69a1.36,1.36,0,0,1-1.22,1.49Z" style="fill:#fff"/></g></g></svg>
      </div>
    </span> -->
  <!-- </li> -->
</template>

<script>
import {eventBus} from './EventBus.js'
import axios from 'axios'
export default {
  name: 'item',
  props: ['model', 'active', 'active'],
  data () {
    return {
      // urlTemp: appUrl + 'service/allMentionsForGupi',
      open: true,
      // activeGuideline: 'Pauta A Uno'
    }
  },
  computed: {
    isFolder: function () {
      return this.model.children &&
        this.model.children.length
    },
    dateFilter: function () {
      return this.$store.getters.loadFilterDate
    }
  },
  methods: {
    // updateLoaderColTwo: function (value) {
    //   this.$store.commit('setshowLoaderColTwo', value)
    // },
    showHideGuideline: function (el, close) {
      console.log(el.length)
      let list = el.guidelines_list
      Object.keys(list).forEach(function (item) {
        console.log(list[item])
        if(close){
          list[item].isFolder = false
          el.isFolder = false
        } else {
          list[item].isFolder = true
          el.isFolder = true
        }
      })
      console.log(Object.keys(el))
    },
    isSelect: function (item) {
      return this.active == item
    },
    setActiveGuideline: function (value) {
      this.$emit('activeGuideline', value)
    },



    isActive: function (value) {
      // if(this.active === value){
      //   console.log(count)
      //   this.model.count = this.model.count + 1
      //   console.log(count)
      // }
      return this.active === value
    },
    toggle: function (el) {
      let vm = this
      console.log('este es: '+el)
      if (this.isFolder) {
        this.open = !this.open;
      } else {
        vm.updateLoaderColTwo(true)
        eventBus.$emit('active', el)
        let itemData = {
          "count": vm.model.count,
          "idChild": vm.model.idChild,
          "idFeed": vm.model.idFeed,
          "idGupi": vm.model.idGupi,
          "name": vm.model.name,
          "state":vm.model.state,
          "date": vm.dateFilter,
          'idMety': vm.model.idMediaType
        }
        axios.post(vm.urlTemp, { dataBlock: [ itemData ] })
        .then(function (response) {
          let res = response.data.mention
          vm.setMentions(res)
          vm.updateLoaderColTwo(false)
        })
        .catch(function (error) {
          vm.updateLoaderColTwo(false)
        })
      }

    },
    setMentions: function (value) {
      this.$store.commit("setDataMentions", value)
    }
  }
}
</script>

<style lang="scss">
  .feed-wrapper{
    text-align: left;
    // padding: .5rem 1rem;
    // background-color: orange;
    margin: 0;
    margin-top: .4rem;
    // border-bottom: .1rem solid red;
    width: 100%;
    box-sizing: border-box;
  }
  .feed-item{
    padding: .5rem 1rem;
    border-bottom: .1rem solid #b5b5b5;
    background-color: #ebeceb;
    display: flex;
    cursor: pointer;
    justify-content: space-between;
    .btns{
      display: flex;
    }
  }
  .guidelines-list{
    display: flex;
    flex-direction: column;
    margin: 0;
  }
  .guidelines-item{
    padding: 0 1rem;
    border-bottom: solid .1rem #dcdcdc;
    background: #f5f5f5;
    /* width: 100%; */
    margin: 0;
    margin-left: 1rem;
    margin: 0 0 0 .6rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    span{
      cursor: pointer;
      padding: .5rem 0;
      width: 100%;
    }
  }
  .guidelines-wrapper{
    margin: 0;
  }
  .block{
    padding: .5rem 0;
  }
  .strongGruideline{
    font-weight: bold;
  }
  .openMopdal{
    transform: rotate(180deg)!important;
  }
  .icon-guide{
    display: flex;
    transition: all .3s;
    transform: rotate(0deg);
  }

.changeHeight-leave-active {
  overflow: hidden!important;
  transition: all .5s;
  max-height: 300px!important;
}

.changeHeight-enter-active {
  overflow: hidden!important;
  transition: all 1s;
  max-height: 300px!important;
}
.changeHeight-enter,
.changeHeight-leave-to
{
  overflow: hidden!important;
  // opacity: 0;
  max-height: 0!important;
}
</style>
