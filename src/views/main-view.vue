<template>
  <header-component @toggleMenu="toggleMenu" :menu-opened="isMenu">
  </header-component>
  <navigation-panel v-if="menuOpened" :selectMenu="selectMenuItem" :selected-button="selectedMenuItem" @toggleMenu="toggleMenu"/>
  <div class="main-view__body">
    <component :is="currentTab" class="component"></component>
  </div>
</template>

<script>
import headerComponent from "@/components/header-component";
import NavigationPanel from "@/components/navigation-panel";
import tabLections from "@/components/tab-lections";
import tabBase from "@/components/tab-base";
export default {
  name: "main-view",
  data() {
    return {
      menuOpened: false,
      menuSelectedItem: 'Base'
    }
  },
  components: {
    NavigationPanel,
    headerComponent,
    tabLections,
    tabBase
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
    },
    currentTab(){
      console.log("tab-" + this.menuSelectedItem.toLocaleLowerCase())
      return "tab-" + this.menuSelectedItem.toLocaleLowerCase()
    }
  }
}
</script>

<style lang="scss" scoped>
  .main-view__body {
    height: 80vh;
    min-width: 800px;
    display: flex;
    justify-content: center;
  }
</style>