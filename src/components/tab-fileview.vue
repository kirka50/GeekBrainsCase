<template>
  <div class="tab-fileview">
    <div class="tab-fileview__back-button">
      Х-Вернуться назад
    </div>
    <div class="tab-fileview__uppper-section">
      <div class="uppper-section__video">
        Тут видео
      </div>
      <div class="uppper-section__transcr">
        Тут транскриппт
      </div>
    </div>
    <div class="tab-fileview__down-section">
      <div class="down-section__glos">
        Тут глоссарий
      </div>
      <div class="down-section__consp">
        Тут конспект
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tab-fileview"
}
</script>

<style lang="scss" scoped>
  .tab-fileview {
    padding: 1vh 2vw;
    width: 100%;
    min-width: 90vw;
    .tab-fileview__uppper-section{
      display: flex;
      justify-content: space-around;
      gap: 10px;
      margin-top: 1vh;
      .uppper-section__video {
        height: 500px;
        width: 800px;
        border: #9C9FB0 solid;
      }
      .uppper-section__transcr {
        border: #9C9FB0 solid;
        width: 800px;
      }
    }
    .tab-fileview__down-section {
      margin-top: 6vh;
      display: flex;
      justify-content: space-around;
      gap: 10px;
      .down-section__glos {
        border: #9C9FB0 solid;
        width: 800px;
      }
      .down-section__consp {
        height: 500px;
        border: #9C9FB0 solid;
        width: 800px;
      }
    }
  }
</style>