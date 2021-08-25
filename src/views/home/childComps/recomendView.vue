<template>
<div class="recommend">
 <div v-for="item in recommends" class="recommend-item" :key="item.sort">
   <a :href="item.link">
     <img :src="item.image" alt="">
   </a>
   <div>{{item.title}}</div>
 </div>
</div>
</template>

<script>
export default {
name: "recomendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style scoped>
.recommend {
  display: flex;
  padding-top: 8px;
  font-size: 12px;
  border-bottom: 5px solid #eeeeee;
}
.recommend-item {
  flex: 1;
  text-align: center;

}
.recommend-item img {
  width: 80%;
  margin-bottom: 5px;
}
</style>