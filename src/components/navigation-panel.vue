<template>
  <div class="nav-panel--overlay">
    <div class="nav-panel">
      Панелька :)
    </div>
  </div>
</template>

<script>
export default {
  name: "navigation-panel",
  props: {
    menuOpened: {
      type: Boolean,
      default: false
    },
  },
}
</script>

<style lang="scss" scoped>
  .nav-panel{
    padding: 0 0 0 20px;
    border-right: solid 1px #D8D8D8;
    position: fixed;
    width: 20vw;
    height: 100%;
  }
</style>