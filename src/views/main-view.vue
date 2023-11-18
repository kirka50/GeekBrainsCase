<template>
  <header-component @toggleMenu="toggleMenu" :menu-opened="isMenu">
  </header-component>
  <navigation-panel v-if="menuOpened"/>
  Контент
</template>

<script>
import headerComponent from "@/components/header-component";
import NavigationPanel from "@/components/navigation-panel";
export default {
  name: "main-view",
  data() {
    return {
      menuOpened: false
    }
  },
  components: {
    NavigationPanel,
    headerComponent
  },
  methods: {
    toggleMenu() {
      this.menuOpened = !this.menuOpened
      console.log(this.menuOpened)
    }
  },
  computed: {
    isMenu(){
      return this.menuOpened
    }
  }
}
</script>

<style lang="scss" scoped>

</style>