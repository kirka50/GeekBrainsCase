<template>
  <div class="time-stamp-text">
    <div v-if="ifInGlossTimeStamp" class="time-stamp-text__text">
      <v-tooltip :text="fileText.timestamp[0].toString() + ' - ' + fileText.timestamp[1].toString()">
        <template v-slot:activator="{ props }">
          <div class="time-stamp-text__text--mod--chip" v-bind="props">
            <div :class="{'red': isTerminCorrect}">
              {{ fileText.text }}
            </div>
          </div>
        </template>
      </v-tooltip>
    </div>
    <div v-else class="time-stamp-text__text">
        <v-tooltip :text="fileText.timestamp[0].toString() + ' - ' + fileText.timestamp[1].toString()">
          <template v-slot:activator="{ props }">
            <div class="time-stamp-text__text--mod" v-bind="props">{{ fileText.text }}</div>
          </template>
        </v-tooltip>
    </div>
  </div>
</template>

<script>

export default {
  name: "time-stamp-text",
  data() {
    return {
      terminName: ''
    }
  },
  props: {
    fileText: {
      type: Object,
    },
    gloss: {
      type: Object,
    },
    selectedTermi : {
    }
  },
  computed: {
    ifInGlossTimeStamp() {
      for (let i in this.gloss) {
        if ((this.fileText.timestamp[0] > this.gloss[i].start) && (this.fileText.timestamp[1] < this.gloss[i].end)) {
          console.log(this.gloss[i])
          console.log(this.fileText.timestamp[0] + ' ' + this.gloss[i].start, this.fileText.timestamp[1] + ' ' + this.gloss[i].end,)
          return true
        }
      }
      return false
    },
    isTerminCorrect() {
      if (this.terminName == this.selectedTermi){
        return true
      } return false
    }
  },
  mounted() {
    for (let i in this.gloss) {
      if ((this.fileText.timestamp[0] > this.gloss[i].start) && (this.fileText.timestamp[1] < this.gloss[i].end)) {
        console.log(this.gloss[i])
        console.log(this.fileText.timestamp[0] + ' ' + this.gloss[i].start, this.fileText.timestamp[1] + ' ' + this.gloss[i].end,)
        this.terminName = this.gloss[i].term
      }
    }
  }, methods: {
    hightlightTermin() {

    }
  },
}
</script>

<style lang="scss" scoped>
.time-stamp-text{
  .red {
    margin: 1px;
    padding: 3px;
    border-radius: 20px;
    background: #ff1d5e;
    color: white;
  }
  .green {
    margin: 1px;
    padding: 3px;
    border-radius: 20px;
    background: lightgreen;
    color: black;
  }
  text-align: left;
  display: flex;
  justify-content: left;
  .time-stamp-text__stamp-start{
    .v-chip {
      font-size: 12px;
      width: 80px;
      display: flex;
      justify-content: center;
      position: relative;
      flex-wrap: wrap;
    }

  }
  .time-stamp-text__text {
    display: flex;
    margin-left: 0.5em;
    .time-stamp-text__text--mod {
      display: flex;
      justify-content: left;
      align-items: flex-start;
      .time-stamp-text__text--mod--chip {


        width: 100%;
        v-chip {
          width: 100%;
        }
      }
    }
  }
  .time-stamp-text__stamp-end {

  }

}
</style>