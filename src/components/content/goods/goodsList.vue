<template>
  <div class="goodslist">
    <goods-item v-for="(gooodsItem, index) in goods" :list="gooodsItem" :key="index"></goods-item>
  </div>
</template>

<script>
import goodsItem from "@/components/content/goods/goodsItem";
export default {
name: "goodList",
  components: {
    goodsItem
  },
  props: {
  goods: {
    type: Array,
    default() {
      return []
    }
  }

  }
}
</script>

<style scoped>
.goodslist {
  width: 100%;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
</style>