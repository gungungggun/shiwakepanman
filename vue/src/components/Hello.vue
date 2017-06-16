<template lang="pug">
  div.wrap
    div
      h1
        img(src="static/title.png")
      router-link(to="start") スタート
</template>

<style lang="stylus" scoped>
.wrap
  width 100%
  height 100%
  display flex
  align-items center
  justify-content center
  flex-wrap wrap
  h1
    width 100%
    display block
  img
    width 80%

a
  color #42b983
  display block
  border 3px solid #42b983
  padding 2% 5%
  margin 0 auto
  width 50%
  text-decoration none
  font-size 8vw
  font-weight bold
  &:active
    color #fff
    background #42b983

</style>
