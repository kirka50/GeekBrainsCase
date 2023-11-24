<template>
  <div v-if="selectedTermi == glossTermin" style="background: #ff1d5e; border-radius: 10px; padding: 5px">
    <h1 @click="hightlightTermin(oneGloss.term)">
      {{oneGloss.term}}
    </h1>
    <p>
      {{ oneGloss.definition }}
    </p>
  </div>
  <div v-else>
    <h1 @click="hightlightTermin(oneGloss.term)">
      {{oneGloss.term}}
    </h1>
    <p>
      {{ oneGloss.definition }}
    </p>
  </div>
</template>

<script>
export default {
  name: "gloss-component",
  data() {
    return {
      glossTermin: this.oneGloss.term
    }
  },
  props: {
    oneGloss: {
      type: Object
    },
    hightlightTermin: {
    },
    selectedTermi: {
    }
  },
}
</script>

<style lang="scss" scoped>
  h1 {
    cursor: pointer;
  }
</style>