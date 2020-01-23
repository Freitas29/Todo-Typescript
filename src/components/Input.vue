<template>
  <input
    v-on="$listeners"
    :value="value"
    @input="$emit('update', $event.target.value)"
  />
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    value: String
  },
  methods: {
    handleInput(): void {
      this.$emit("input", this.value);
    }
  },
  model: {
    prop: "value",
    event: "update"
  }
});
</script>

<style scoped>
.input {
  width: auto;
}
</style>
