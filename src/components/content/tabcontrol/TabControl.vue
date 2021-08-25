<template>
  <div class="tabcontroll">
    <div class="tabcontroll-item"
         v-for="(item, index) in titles"
         :key="item"
         @click="ClickItem(index)" :class="{active: index === currentIndex}">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  data() {
    return {
      currentIndex: 0
    }
  },
  props: {
    titles: {
      type: Array,
      default() {
        return []
      }
    }
  },
  methods: {
    ClickItem(index) {
      this.currentIndex = index;
      this.$emit('tabClick', index)
    }
  }
}
</script>

<style scoped>
.tabcontroll {
  width: 100%;
  display: flex;
  text-align: center;
  height: 40px;
  line-height: 40px;
}
.tabcontroll-item {
  flex: 1;
  font-size: 14px;
}
.tabcontroll-item span {
  padding: 5px;
}
.active {
  color: var(--color-high-text);
}
.active span {
  border-bottom: 3px solid var(--color-high-text);
}
</style>