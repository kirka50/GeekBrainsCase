<template>
  <header-component @toggleMenu="toggleMenu" :menu-opened="isMenu">
  </header-component>
  <navigation-panel v-if="menuOpened" :selectMenu="selectMenuItem" :selected-button="selectedMenuItem"/>
  Контент
</template>

<script>
import headerComponent from "@/components/header-component";
import NavigationPanel from "@/components/navigation-panel";
export default {
  name: "main-view",
  data() {
    return {
      menuOpened: false,
      menuSelectedItem: ''
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
    },
    selectMenuItem(item) {
      this.menuSelectedItem = item
      console.log(item)
    }
  },
  computed: {
    isMenu(){
      return this.menuOpened
    },
    selectedMenuItem() {
      return this.menuSelectedItem
    }
  }
}
</script>

<style lang="scss" scoped>

</style>