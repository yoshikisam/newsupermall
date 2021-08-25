<template>
<div id="home">
  <nav-bar class="home-nav">
  <template v-slot:center>
    购物街
  </template>
</nav-bar>
  <scroller ref="scroller"
            class="content"
            :pull-up-load="true"
            @pullingUp="loadMore" @scroll="getPosition">
    <home-swiper :banners="banners">

    </home-swiper>
    <recomend-view :recommends="recommends"></recomend-view>
    <feature-view></feature-view>
    <tab-control :titles="titles" class="home-tabcontroll" @tabClick="tabClick"></tab-control>
    <goods-list :goods="showGoods"></goods-list>
  </scroller>
<back-top class="back-top" v-show="isBackTop" @click.native="scrollTo"></back-top>
</div>
</template>

<script>
import navBar from "@/components/common/navBar/navBar";
import HomeSwiper from "@/views/home/childComps/HomeSwiper";
import recomendView from "@/views/home/childComps/recomendView";
import featureView from "@/views/home/childComps/featureView";
import TabControl from "@/components/content/tabcontrol/TabControl";
import goodsList from "@/components/content/goods/goodsList";
import scroller from "@/components/common/scroller/scroller";
import backTop from "@/components/content/backtop/backTop";
import {getHomeMultidata, getHomeGoods} from "@/network/home";



export default {
name: "Home",
  components: {
    navBar,
    HomeSwiper,
    recomendView,
    featureView,
    TabControl,
    goodsList,
    scroller,
    backTop
  },
  data() {
  return {
    banners: [],
    recommends: [],
    titles: ['流行', '新款', '精选'],
    goods: {
      'pop': {page: 0, list: []},
      'new': {page: 0, list: []},
      'sell': {page: 0, list: []}
    },
    currentType: 'pop',
    isBackTop: false//显示返回顶部按钮
  }
  },
  created() {
  //首页创建完请求数据
    this.getHomeMultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  mounted() {
    const refresh = this.debounce(this.$refs.scroller.refresh, 200)
    this.$bus.$on('itemImageLoad', () => {
      refresh()
    })
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list
    }
  },
  methods: {
  //防抖
    debounce(func, delay) {
      let timer = null
      return function (...args) {
        if(timer) clearTimeout(timer)
        timer = setTimeout(() => {
          func.apply(this, args)
        }, delay)
      }
    },
  //监听方法
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = 'pop'
              break
        case 1:
          this.currentType = 'new'
              break
        case 2:
          this.currentType = 'sell'
              break
      }
    },
    getPosition(positon) {
      this.isBackTop = -positon.y > 1000;
    },
    loadMore() {
      // console.log('load')
      this.getHomeGoods(this.currentType)//上拉刷新
      // this.$refs.scroller.scroller.refresh()
    },
    scrollTo() {
      this.$refs.scroller.scrollTo()
    },
  //网络请求
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        // console.log(res)
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      }).catch()
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        // console.log(res)
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
        this.$refs.scroller.finishPullUp()
      })
    }
  }
}
</script>

<style scoped>
#home {
  height: 100vh;
  position: relative;
  padding-top: 44px;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
#home .content {
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
.home-tabcontroll {
  position: sticky;
  top: 44px;
  z-index: 9;
}
.back-top {
  position: absolute;
  bottom: 50px;
  right: 5px;
}
</style>