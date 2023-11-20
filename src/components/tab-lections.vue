<template>
  <div class="tab-lections"
       @drop="dragDrop">
    <div class="tab-lections__file-upload"
         @dragover="onDragOver"
         @dragleave="onDragLeave">
      <div class="file-upload">
        <div v-if="isDrag">
          Бросьте файл сюда
        </div>
        <div v-else>
          Я и есть загрузка файлов кста
          <div>
            Или
          </div>
          <label class="file-upload__upload-button">
            Загрузите файл
            <input type="file" ref="file" @change="onChange">
          </label>
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
      myFile: ''
    }
  },
  methods: {
    dragDrop(e) {
      console.log(e.dataTransfer.files)
      e.preventDefault();
      this.myFile = e.dataTransfer.files;
      this.isDrag = false;

    },
    onChange() {
      this.myFile = this.$refs.file.files;
    },
    onDragOver(e) {
      e.preventDefault()
      this.isDrag = true
    },
    onDragLeave(e) {
      e.preventDefault()
      this.isDrag = false
    }
  },

}
</script>

<style lang="scss" scoped>
.tab-lections {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  min-height: 300px;
  .tab-lections__file-upload {
    border: dotted gray 1px;
    border-radius: 20px;
    height: 40vh;
    width: 50vh;
    min-height: 300px;
    min-width: 500px;
    .file-upload {
      gap: 10px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100%;
      text-align: center;
      .file-upload__upload-button {
        border: 1px solid #ccc;
        display: inline-block;
        padding: 6px 12px;
        cursor: pointer;
        color: white;
        border-radius: 20px;
        background-color: #8D46F6;
        input[type="file"] {
          display: none;
        }
      }
      .file-upload__upload-button:hover {
        background-color: #6404ff;
      }
    }
  }
}
</style>