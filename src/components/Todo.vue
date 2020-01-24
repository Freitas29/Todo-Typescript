<template>
  <div
    :class="['todo', todo.finished ? 'completed' : 'notCompleted']"
    @click="handleTodo(todo)"
  >
    <p>{{ todo.name }}</p>

    <span class="float-button" @click="remove">&#128500;</span>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { TodoInterface } from "../types/todo";

export default Vue.extend({
  name: "Todo" as string,
  props: {
    todo: Object
  },
  methods: {
    handleTodo(todo: TodoInterface): void {
      todo.finished = !todo.finished;
    },
    remove(): void {
      this.$emit("removed", this.todo);
    }
  }
});
</script>

<style lang="sass" scoped>
$success: #27ce7a

.todo
    background-color: red
    min-height: 120px
    height: auto
    width: 100%
    border-radius: 5px
    color: #fff
    display: flex
    align-items: center
    justify-content: center
    font-size: 16px
    font-weight: 600
    text-transform: capitalize
    transition: all 0.5s
    cursor: pointer
    position: relative

    &:hover
      transform: scale(1.1)

.notCompleted
  background-color: #eb4d4b

.completed
  background-color: #6ab04c
  text-decoration: line-through

.float-button
  font-size: 30px
  position: absolute
  top: 0px
  right: 10px
  z-index: 99
</style>
