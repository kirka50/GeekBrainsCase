<template>
  <div class="tab-base">
    <div v-if="loading" class="tab-base__loading">
      <v-progress-circular indeterminate></v-progress-circular>
    </div>
    <div v-else>
      <div v-if="lecturesList != ''" class="tab-base__content">
        <template v-for="i in lecturesList" :key="i">
          <file-preview :file="i" :select-menu="selectMenu" :select-file-id="selectFileId"/>
        </template>
      </div>
      <div v-else>
        Пусто, возможно вы не загрули никаких лекций
      </div>

    </div>
  </div>
</template>

<script>
import filePreview from "@/components/file-preview";
import axios from "axios";
export default {

  name: "tab-base",
  components: {filePreview},
  data() {
    return {
      loading: true,
      lecturesList: ''
    }
  },
  props: {
    selectMenu: {
    },
    selectFileId: {
    }
  },
  beforeCreate() {
    this.loading = true
    axios.get('https://geekbrains.sosus.org/v1/lectures/', {
      headers: {
        'accept': 'application/json'
      }})
        .then(response => {
          if (response.data.length === 0) {
            console.log(this.lecturesList)
            this.lecturesList = ''
          }
          this.lecturesList = response.data
          this.loading = false
        })
        .catch(reason => {
          console.log('Ошибка загрузки', reason)
        })
  },
  methods: {
    checkStatus() {
      for (let i in this.lecturesList) {
        if (this.lecturesList[i].status != 'Processed') {
          axios.get(`https://geekbrains.sosus.org/v1/lectures/${this.lecturesList[i].id}/status/`)
              .then(response => {
                if (response.data.status == 'Processed') {
                  this.changeStatusById(this.lecturesList[i].id)
                }
              })
              .catch(reason => {
                console.log('Ошибка загрузки', reason)
              })
        }
      }
    },
    changeStatusById(id){
      for (let i in this.lecturesList) {
        if (this.lecturesList[i].id === id) {
          this.lecturesList[i].status = 'Processed'
        }
      }
    },
    updateList() {
      axios.get('https://geekbrains.sosus.org/v1/lectures/', {
        headers: {
          'accept': 'application/json'
        }}).then(response => {
          this.lecturesList = response.data
      })
          .catch(reason => {
            console.log('Ошибка загрузки', reason)
          })
    }
  },
  mounted: function () {
    this.timer = setInterval(() => {
      this.updateList()
    }, 5000)
  },
  beforeUnmount() {
    clearInterval(this.timer)
  }
}
</script>

<style lang="scss" scoped>
  .tab-base{
    height: 100%;
    width: 100%;
    display: flex;
    padding: 0 5vw;
    margin-top: 10vh;
    gap: 40px;
    flex-direction: row;
    justify-content: flex-start;
    flex-wrap: wrap;
    .tab-base__loading {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      width: 100%;
    }
    .tab-base__content {
      height: 100%;
      width: 100%;
      display: flex;
      padding: 0 5vw;
      gap: 40px;
      flex-direction: row;
      justify-content: flex-start;
      flex-wrap: wrap;
    }
  }
</style>