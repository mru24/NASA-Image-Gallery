<template>
  <div>
    <div class="container">
      <h2 class="title">
        <img src="../assets/nasa-logo.png" alt="" width="120px">
        Image Gallery
      </h2>
      <div class="content">
        <h4 class="query">{{ query }}</h4>
        <transition-group tag="ul" mode="out-in">
          <li v-for="(item, index) in items" :key="index">
            <img :src="item.links[0].href" alt="" width="200px" @mouseover="showInfo=true">
            <div class="info" v-if="showInfo">
              <p v-html="item.data[0].description"></p>
            </div>
          </li>
        </transition-group>
      </div>
      <div class="search">
        <form v-on:submit.prevent="getResult(query)">
          <input type="text" v-model="query">
          <button type="submit">
            <img src="../assets/search.png" alt="" width="28px">
          </button>
        </form>
      </div>
    </div>
    <div class="footer">
        WWPROJECT STUDIO &copy; 2018
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      query: '',
      items: '',
      showInfo: false
    }
  },
  methods: {
    getResult (query) {
      this.noitems = 10
      axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image')
        .then(response => {
          var collection = response.data.collection.items
          console.log(collection)
          this.items = collection
        })
    }
  },
  created () {
    this.getResult('earth')
  }
}
</script>

<style lang="sass" scoped>
@import 'config'

.title
  margin: 20px 0
  text-align: center
  font-size: 40px
  letter-spacing: 3px
  font-weight: 300
  display: flex
  justify-content: center
  align-items: center
.query
  margin: 10px 0
  padding: 5px 0
  font-size: 30px
  text-transform: capitalize
  text-align: center
  border-bottom: 1px solid #999
.search
  position: fixed
  bottom: 30px
  left: 30px
  width: 100%
  form
    width: 100%
    input
      width: 50%
      height: 35px
      padding-left: 20px
      font-size: 22px
      border: none
      border-radius: 5px
      @include bp-mobileSM
        width: 70%
    button
      position: relative
      top: 6px
      left: -12px
      width: 60px
      height: 35px
      background: white
      border: none
      border-radius: 0 5px 5px 0
      border-left: 1px solid #999
      cursor: pointer

.content
  margin: 50px 0
  ul
    column-count: 4
    column-gap: 5px
    @include bp-mobile
      column-count: 3
    @include bp-mobileSM
      column-count: 2
    li
      img
        width: 100% !important
        height: auto
        transition: .4s
        &:hover
          opacity: 1
      .info
        position: fixed
        z-index: 9999
        left: 0
        top: -200%
        width: 100%
        padding: 40px 20px
        background: rgba(#282828, 0.7)
        color: white
        transition: .6s
        pointer-events: none
        p
          font-family: 'Roboto', sans-serif
          font-size: 20px
          font-weight: 300
      img:hover ~ .info
        top: 0

.content:hover img
  opacity: .3

.footer
  height: 180px
  display: flex
  justify-content: center
  align-items: center
  color: #999

.v-enter-active, .v-leave-active
  transition: all .5s
.v-enter, .v-leave-to
  opacity: 0
  transform: translateY(30px)
</style>
