<template lang="pug">
  div#app
    transition(name="start" mode="out-in")
      router-view
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang="stylus">
html, body
  padding 0
  margin 0
  width 100%
  height 100%
  overflow hidden
  -webkit-text-size-adjust: 100%;
#app
  height 100%
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

.start-enter-active
  animation-name enter
  animation-duration 1.5s

@keyframes enter
  0%
    opacity 0
  100%
    opacity 1
</style>
