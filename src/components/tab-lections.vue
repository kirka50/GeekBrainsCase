<template>
  <div v-if="isLoading">
    <div class="loading-overlay">
      <div class="circles-to-rhombuses-spinner">
        <div class="circle"></div>
        <div class="circle"></div>
        <div class="circle"></div>
      </div>
    </div>
  </div>

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
            <input type="file" ref="file" @change="initFileLoad">
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
function delay(milliseconds){
  return new Promise(resolve => {
    setTimeout(resolve, milliseconds);
  });
}
function getUUID(fileName) {
  let result
  axios.get('/',fileName).then(response => (result = response))
  return result
}
export default {
  name: "tab-lections",
  data() {
    return {
      isDrag: false,
      myFile: '',
      isLoading: false,
      fileUUID: ''
    }
  },
  methods: {
    dragDrop(e) {
      e.preventDefault();
      this.initFileLoad(e)
    },
    onDragOver(e) {
      e.preventDefault()
      this.isDrag = true
    },
    onDragLeave(e) {
      e.preventDefault()
      this.isDrag = false
    },
    setLoadingFalse() {
      this.isLoading = false
    },
    initFileLoad(e){
      this.isDrag = false;
      this.isLoading = true
      this.myFile = e.dataTransfer.files
      let fileData = getUUID(e.dataTransfer.files[0].name)
    },
    loadFile(e,fileData){
      axios.post(fileData.upload_url,e.dataTransfer.files)
          .then(response => console.log('Получилось'))
      this.startAnalyze(fileData)
    },
    startAnalyze(fileData) {
      axios.post(`/${fileData.id}/start_analyze`).then(response => console.log('анализ'))
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
.circles-to-rhombuses-spinner, .circles-to-rhombuses-spinner * {
  box-sizing: border-box;
}
.loading-overlay {
  height: 100vh;
  width: 100vw;
  background: rgba(0, 0, 0, 0.8);
  position: fixed;
  top: 0;
  left: 0;
}
.circles-to-rhombuses-spinner {
  height: 100vh;
  width: calc( (15px + 15px * 1.125) * 3);
  top: 50vh;
  left: 48vw;
  display: flex;
  position: fixed;

}

.circles-to-rhombuses-spinner .circle {
  height: 15px;
  width: 15px;
  margin-left: calc(15px * 1.125);
  transform: rotate(45deg);
  border-radius: 10%;
  border: 3px solid #ff1d5e;
  overflow: hidden;
  background: transparent;

  animation: circles-to-rhombuses-animation 1200ms linear infinite;
}

.circles-to-rhombuses-spinner .circle:nth-child(1) {
  animation-delay: calc(150ms * 1);
  margin-left: 0
}

.circles-to-rhombuses-spinner .circle:nth-child(2) {
  animation-delay: calc(150ms * 2);
}

.circles-to-rhombuses-spinner .circle:nth-child(3) {
  animation-delay: calc(150ms * 3);
}

@keyframes circles-to-rhombuses-animation {
  0% {
    border-radius: 10%;
  }

  17.5% {
    border-radius: 10%;
  }

  50% {
    border-radius: 100%;
  }


  93.5% {
    border-radius: 10%;
  }

  100% {
    border-radius: 10%;
  }
}

@keyframes circles-to-rhombuses-background-animation {
  50% {
    opacity: 0.4;
  }
}
</style>