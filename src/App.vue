<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from './components/Main'

export default {
  components: {
    Main
  }
}
</script>

<style lang="sass">
@import './components/config'
// FONTS
@import url('https://fonts.googleapis.com/css?family=Roboto:300,700')

*
  margin: 0
  padding: 0
  box-sizing: border-box

li
  list-style: none
a, a:visited, a:active
  text-decoration: none
  color: inherit

body
  background: #2e2d33
  font-family: "Roboto", sans-serif
  color: #d5d5d5
  .container
    width: 75%
    margin: auto
    @include bp-mobile
      width: 80%
    @include bp-mobileSM
      width: 95%
</style>
