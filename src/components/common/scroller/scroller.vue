<template>
<div ref="wrapper">
<div>
  <slot></slot>
</div>
</div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "scroller",
  data() {
    return {
      scroller: {
        type: Object,
        default() {
          return {}
        }
      }
    }
  },
  props: {
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  mounted() {
    this.scroller = new BScroll(this.$refs.wrapper, {
      probeType: 2,
      click: true,
      pullUpLoad: this.pullUpLoad,
      mouseWheel: true,
      observeDOM: true,//根据dom变化刷新
      observeImage: true//根据图片加载完成刷新
    })

    this.scroller.on('pullingUp', () => {
      this.$emit('pullingUp')
    })
    this.scroller.on('scroll', (position) => {
      this.$emit('scroll', position)
    })
  },
  methods: {
    finishPullUp() {
      this.scroller && this.scroller.finishPullUp()
    },
    scrollTo(x, y, time=300) {
      this.scroller && this.scroller.scrollTo(0, 0, time)
    },
    refresh() {
      console.log('--')
      this.scroller && this.scroller.refresh()
    }
  }
}
</script>

<style scoped>

</style>