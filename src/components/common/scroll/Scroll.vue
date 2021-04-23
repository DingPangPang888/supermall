<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BSscroll from 'better-scroll'

	export default {
		name: "Scroll",
    props: {
		  probeType: {
        Number,
        default: 0
      },
      pullUpLoad: {
		    type: Boolean,
        default: false
      }
    },
    data() {
		  return {
		    scroll: null,
        message: '哈哈哈哈'
      }
    },
    mounted() {
		  //1.创建BScroll对象
		  this.scroll = new BSscroll(this.$refs.wrapper, {
        click: true,
        probeType: this.probeType,
        pullUpLoad: this.pullUpLoad,
        //监听图片加载完成
        // observeDOM: true,
        // observeDOMImage: true
      })
      //2.监听滚动的位置(代码更加严谨)
       if (this.probeType === 2 || this.probeType === 3) {
         this.scroll.on('scroll', (position) => {
           this.$emit('scroll', position)
         })
       }
      //3.监听上拉事件（代码更加严谨）
      if (this.pullUpLoad) {
        this.scroll.on('pullingUp', () => {
          this.$emit('pullingUp')
        })
      }
    },
    methods: {
		  scrollTo(x, y, time=300) {
		    this.scroll && this.scrollTo && this.scroll.scrollTo(x, y, time)
      },
      refresh() {
        this.scroll && this.scrollTo && this.scroll.refresh()
      },
      finishPullUp() {
        this.scroll && this.scroll.finishPullUp()
      },
      getScrollY() {
		    return this.scroll ? this.scroll.y : 0
      }
    }
  }
</script>

<style scoped>

</style>
