<template>
  <div class="file-preview">
    <div class="file-preview__title">
      <img :src="require('@/assets/preview-title-prototype.png')">
    </div>
    <div class="file-preview__name">
      Я крутой и с большой пипиркой
    </div>
  </div>
</template>

<script>
export default {
  name: "file-preview"
}
</script>

<style lang="scss" scoped>
  .file-preview {
    cursor: pointer;
    .file-preview__title {
      img {
        height: 200px;
        width: auto;
        border-radius: 20px;
      }
    }
  }
</style>