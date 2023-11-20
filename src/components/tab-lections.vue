<template>
  <div class="tab-lections">
    <div class="tab-lections__file-upload"
         @drop="dragDrop"
         @dragover="this.isDrag = true"
         @dragleave="this.isDrag = false">
      <div class="file-upload">
        <div v-if="isDrag">
          Бросьте файл сюда
        </div>
        <div v-else>
          Я и есть загрузка файлов кста
          <div>
            Или
          </div>
          <div class="file-upload__upload-button">
            <input type="file" ref="file" name="file" @change="onChange">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tab-lections",
  data() {
    return {
      isDrag: false,
      file: ''
    }
  },
  methods: {
    dragDrop(e) {
      e.preventDefault();
      this.$refs.file.files = e.dataTransfer.files;
      this.onChange();
      this.isDrag = false;
      console.log('drop')
    },
    onChange() {
      this.file = this.$refs.file.files;
    },
  },

}
</script>

<style lang="scss" scoped>
.tab-lections {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;

  .tab-lections__file-upload {
    border: dotted gray 1px;
    border-radius: 20px;
    height: 40vh;
    width: 50vh;

    .file-upload {
      gap: 10px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100%;

    }
  }
}
</style>