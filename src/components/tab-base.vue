<template>
  <div class="tab-base">
    <template v-for="i in [...Array(temp).keys()]" :key="i">
      <file-preview/>
    </template>
  </div>
</template>

<script>
import filePreview from "@/components/file-preview";
export default {
  name: "tab-base",
  components: {filePreview},
  data() {
    return {
      temp: 20
    }
  },
}
</script>

<style scoped>
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
  }
</style>