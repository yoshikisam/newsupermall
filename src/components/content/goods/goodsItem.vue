<template>
  <div class="goodsitem">
    <a :href="list.link"><img :src="list.show.img" alt="" class="img" @load="imageLoad"></a>
    <div class="goodsitem-info">
      <p>{{list.title}}</p>
      <span class="price">{{list.price}}</span>
      <span class="collect">{{list.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "goodsItem",
  props: {
    list: {
      type: Object,
      default() {
        return {}
      }
    },
  },
  methods: {
    imageLoad() {
      this.$bus.$emit('itemImageLoad')
    }
  }
}
</script>

<style scoped>
.goodsitem {
  width: 46%;
  margin-bottom: 10px;
}
.goodsitem .img {
  width: 100%;
  border-radius: 2px;
}
.goodsitem-info {
  text-align: center;
  margin-top: 5px;
  font-size: 14px;
}
.goodsitem-info p{
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.goodsitem-info .price {
  margin-right: 16px;
  color: var(--color-high-text);
}
.goodsitem-info .collect {
  position: relative;
}
.collect::before {
  content: '';
  position: absolute;
  left: -15px;
  top: 0px;
  width: 14px;
  height: 14px;
  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
</style>