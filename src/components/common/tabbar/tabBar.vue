<template>
  <div id="tar-bar">
    <slot></slot>
  </div>
</template>

<script>
export default {
name: "tabBar",
}
</script>

<style scoped>
#tar-bar {
  display: flex;
  position: fixed;
  left: 0;
  bottom: 0;
  background-color: #f6f6f6;
  right: 0;
  box-shadow: 0 -1px 1px rgba(100,100,100,.2);
}
</style>