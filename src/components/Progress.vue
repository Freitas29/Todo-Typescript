<template>
  <div class="progress">
    <p>{{ `${percentValue}%` }}</p>
    <div class="percent" :style="{ width: `${percentValue}%` }"></div>
  </div>
</template>

<script lang="ts">
interface progressInterface {
  percent: number;
}

import Vue from "vue";
export default Vue.extend({
  props: {
    percent: Number
  },
  computed: {
    percentValue(): String {
      return this.percent.toFixed(0);
    }
  }
});
</script>

<style lang="sass" scoped>
$heigth-progress: 30px;

.progress
    width: 100%
    height: $heigth-progress
    border: 0.5px solid #EFEFFE;
    position: relative


    p
      position: absolute
      left: 50%
      top: -30%
      color: #fff

    .percent
      height: $heigth-progress
      background: #182C61;
</style>
