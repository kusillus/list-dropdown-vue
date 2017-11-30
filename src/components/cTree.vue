<template>
    <div>
      <div class="feed-wrapper" v-for="item in model" :key="item.feed_name">
        <div class="feed-item">
          {{item.feed_name}}
          <div class="btns">
            <i class="folder" v-if="item.isFolder" @click="showHideGuideline(item, true)">
              <svg style="width:20px;height:20px;fill:white;" viewBox="0 0 24 24">
                <path d="M22,4A2,2 0 0,1 24,6V16A2,2 0 0,1 22,18H6A2,2 0 0,1 4,16V4A2,2 0 0,1 6,2H12L14,4H22M2,6V20H20V22H2A2,2 0 0,1 0,20V11H0V6H2M6,6V16H22V6H6Z" />
              </svg>
            </i>
            <i class="folder" v-else @click="showHideGuideline(item, false)">
              <svg style="width:20px;height:20px;fill:white;" viewBox="0 0 24 24">
                <path d="M20,18H4V8H20M20,6H12L10,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V8C22,6.89 21.1,6 20,6Z" />
              </svg>
            </i>
            <i class="icon-guide" :class="{openMopdal: !item.isOpen}" @click="item.isOpen=!item.isOpen">
                <svg style="width:24px;height:24px;fill:white;" viewBox="0 0 24 24">
                  <path d="M7,10L12,15L17,10H7Z" />
                </svg>
              </i>
          </div>
        </div>
        <transition name="changeHeight" mode="out-in">
        <ul v-if="item.isOpen" class="guidelines-list">
          <li class="guidelines-wrapper" v-for="el in item.guidelines_list" :key="el.guideline_name">
            <div class="guidelines-item">
              <span :class="{strongGruideline: isSelect(el.guideline_name)}" @click="setActiveGuideline(el)">{{el.guideline_name}} - {{el.guideline_count}}</span>
              <i class="icon-guide" :class="{openMopdal: !el.isFolder}" @click="el.isFolder=!el.isFolder">
                <svg style="width:24px;height:24px;" viewBox="0 0 24 24">
                  <path d="M7,10L12,15L17,10H7Z" />
                </svg>
              </i>
            </div>
            <transition name="changeHeight" mode="out-in">
              <div style="padding-left: 2rem;" v-if="el.isFolder">
                <div
                  class="block"
                  v-for="block in el.blocks_list"
                  :key="block.block_name">
                  {{block.block_name}}
                  <span class="count">
                    ({{block.block_count}})
                  </span>
                </div>
              </div>
            </transition>
          </li>
        </ul>
        </transition>
      </div>
    </div>
</template>

<script>
import {eventBus} from './EventBus.js'
import axios from 'axios'
export default {
  name: 'item',
  props: ['model', 'active', 'active'],
  data () {
    return {
      open: true,
    }
  },
  methods: {
    showHideGuideline: function (el, close) {
      let guideSize = el.guidelines_list.length
      let list = el.guidelines_list
      let valueTrue = 0
      let valueFalse = 0
      let openList = close
      Object.keys(list).forEach(function (i) {
        if(list[i].isFolder) {
          valueTrue = valueTrue + 1
        } else {
          valueFalse = valueFalse + 1
        }
      })
      if(close) {
        if(valueFalse == guideSize) {
          openList = false
        }
      } else {
        if(valueTrue == guideSize) {
          openList = true
        }
      }
      Object.keys(list).forEach(function (item) {
        if(openList){
          list[item].isFolder = false
          el.isFolder = false
        } else {
          list[item].isFolder = true
          el.isFolder = true
        }
      })
    },
    isSelect: function (item) {
      return this.active == item
    },
    setActiveGuideline: function (value) {
      this.$emit('activeGuideline', value)
    }
  }
}
</script>

<style lang="scss">
  .feed-wrapper{
    text-align: left;
    margin: 0;
    margin-top: .4rem;
    width: 100%;
    box-sizing: border-box;
  }
  .feed-item{
    padding: .5rem 1rem;
    border-bottom: .1rem solid #0087d6;
    background-color: #04a3ff;
    display: flex;
    cursor: default;
    color:white;
    font-weight: bold;
    justify-content: space-between;
    align-items: center;
    .btns{
      display: flex;
      align-items: center;
      .folder{
        padding-right: .5rem;
        display: flex;
        cursor: pointer;
      }
    }
  }
  .count{
    font-size: 0.9rem;
    margin-left: .5rem;
    color: #b9b9b9;
    font-weight: 900;
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
    cursor: default;
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
    cursor: pointer;
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
