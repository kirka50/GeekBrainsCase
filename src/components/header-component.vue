<template>
  <div class="header">
    <div class="header__body">
      <div class="body__left-side">
        <div class="left-side__menu-button" @click="this.$emit('toggleMenu')">
          <img :src="require('@/assets/burger-button-opened.svg')" v-if="menuOpened">
          <img :src="require('@/assets/burger-buton.svg')" v-else class="left-side__menu-button--opened">
        </div>
        <div class="left-side__logo">
          <img :src="require('@/assets/GeekBrainsLogo.svg')">
        </div>
      </div>
      <div class="body__right-side">
        <div class="right-side__help-ico">
          <img :src="require('@/assets/help-ico.svg')" alt="11">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "header-component",
  data() {
    return {
    }
  },
  props: {
    menuOpened: {
      type: Boolean,
      default: false
    },
  },
}
</script>

<style lang="scss" scoped>
  .header {
    border-bottom: solid 1px #D8D8D8;
    .header__body{
      margin: 20px 10px 0 20px;
      display: flex;
      flex-direction: row;
      gap: 10px;
      justify-content: space-between;
      .body__left-side {
        display: flex;
        flex-direction: row;
        gap: 10px;
        align-items: center;
        .left-side__logo {
          img {
            height: 40px;
            width: auto;
          }
        }
        .left-side__menu-button {
          img {
            height: 40px;
            width: 40px;
            cursor: pointer;
          }
         .left-side__menu-button--opened {
           img {
             height: 40px;
             width: 40px;
             cursor: pointer;
           }
         }
        }
      }
    }
    .body__right-side {
      display: flex;
      align-items: center;
      .right-side__help-ico {
        img  {
          height: 30px;
          width: auto;
          cursor: pointer;
        }
      }
    }
  }
</style>