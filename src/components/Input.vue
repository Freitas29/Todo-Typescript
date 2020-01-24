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

<style lang="sass" scoped>
input
  width: 80%
  height: 48px
  outline: none
  border: none
  background-color: #686de0
  border: 1px solid rgb(255, 255, 255)
  color: #efefef
  font-size: 20px
  border-radius: 10px;
  padding: 0px 20px;
  transition: all 0.5s;

  &:focus
    background-color: rgb(255, 255, 255)
    border: 1px solid #686de0
    color: rgb(11, 10, 13)
    width: 100%
</style>
