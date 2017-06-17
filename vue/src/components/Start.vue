<template lang="pug">
  div.inner
    header
      div.result(v-if="result !== null")
        p.success(v-if="result") O
        p(v-else) X
      div.score
        div.success
          span.mark O
          span {{ score.success }}
        div.failed
          span.mark X
          span {{ score.failed }}
    main
      v-touch.view(v-on:swipeleft="onSwipeLeft" v-on:swiperight="onSwipeRight")
        div.items(:class="{ left: !action, right: action }")
          transition(v-for="(item, index) in list"  name="char" mode="out-in")
            div.item(:style="{backgroundImage: 'url(static/' + master[item].name + '.png'}" v-if="index===count")
    footer
      div.box.left(:style="{background: master[select[0]].color}" @click="onSwipeLeft")
        img(:src="'static/' + master[select[0]].name + '.png'")
        p {{ select[0]  }}
      div.box.right(:style="{background: master[select[1]].color}" @click="onSwipeRight")
        img(:src="'static/' + master[select[1]].name + '.png'")
</template>

<script>
export default {
  mounted: function () {
    this.generate()
  },
  data () {
    return {
      master: [
        {
          name: "anpanman",
          color: "#f10000"
        },
        {
          name: "baikinman",
          color: "#5e0094"
        },
        {
          name: "dokinchan",
          color: "#ff6600"
        },
        {
          name: "karepanman",
          color: "#9c6d4b"
        },
        {
          name: "shokupanman",
          color: "#ffffff"
        },
        {
          name: "jamojisan",
          color: "#dcfffc"
        },
        {
          name: "batako",
          color: "#005998"
        },
        {
          name: "chizu",
          color: "#ffca35"
        },
        {
          name: "kokinchan",
          color: "#00a0e0"
        },
        {
          name: "horaman",
          color: "#8f5396"
        },
        {
          name: "meronpanna",
          color: "#d3ffb2"
        },
        {
          name: "rorupanna",
          color: "#1d0838"
        },
        {
          name: "kurimupanda",
          color: "#ffcf78"
        },
        {
          name: "akachanman",
          color: "#ff5be3"
        },
        {
          name: "komusubiman",
          color: "#ffeeee"
        },
        {
          name: "omusubiman",
          color: "#fffefe"
        }
      ],
      count: 0,
      score: {
        success: 0,
        failed: 0
      },
      select: [],
      list: [],
      result: null,
      action: 1
    }
  },
  methods: {
    generate: function () {
      let rand1 = Math.floor( Math.random() * this.master.length )
      let rand2 = Math.floor( Math.random() * this.master.length )
      while (rand2 === rand1) {
        rand2 = Math.floor( Math.random() * this.master.length )
      }
      this.select = [rand1, rand2]

      this.list = []
      for (let i = 0; i < 3; i++) {
        let rand = Math.floor( Math.random() * this.select.length )
        this.list.push(this.select[rand])
      }

      this.count = 0
    },
    onSwipeLeft: function () {
      this.swipe(0)
    },
    onSwipeRight: function () {
      this.swipe(1)
    },
    swipe: function (num) {
      this.action = num
      if (this.select[num] === this.list[this.count]) {
        this.result = 1
        this.score.success++
      } else {
        this.result = 0
        this.score.failed++
      }
      this.count++

      if (this.count === this.list.length) {
        this.generate()
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
.inner
  height 100%
main
  display flex
  justify-content center
  align-items center
  height calc(100% - 10vh)
  .view
    width 100%
    height 100%
    padding 0 2%
    display flex
    align-items center
    .items
      position relative
      width 100%
      height 100%
      .item
        position absolute
        width 100%
        height 100%
        background-repeat no-repeat
        background-position center
        background-size 80%

.char-enter-active
  animation-name char-enter
  animation-duration 0.5s
  animation-timing-function ease-out

.char-leave-active
  animation-duration 0.5s
  animation-timing-function ease-out
  .left &
    animation-name char-leave-left
  .right &
    animation-name char-leave-right

@keyframes char-enter
  0%
    transform scale(0)
    opacity 0
  100%
    transform scale(1)
    opacity 1

@keyframes char-leave-left
  0%
    transform scale(1)
    top 0
    right 0
  100%
    transform scale(0.2)
    top 400px
    right 30%

@keyframes char-leave-right
  0%
    transform scale(1)
    top 0
    left 0
  100%
    transform scale(0.2)
    top 400px
    left 30%

header
  position fixed
  width 100%
  margin 0 auto
  padding 5% 0
  top 0
  .result
    p
      color #f00
      font-size 80px
      margin 0
      &.success
        color #00f
  .score
    position absolute
    top 2%
    right 2%
    .success
      .mark
        color #00f
    .failed
      .mark
        color #f00

footer
  position fixed
  bottom 0
  display flex
  width 100%
  height 7vh
  min-height 80px
  .box
    width 50%
    height 100%
    border-top 1px solid #333
    img
      height 100%
</style>
