<template>
  <div id="app">
    <h1>Tarefas</h1>
    <div class="div-progress">
      <Progress :percent="percent" class="progress-width" />
    </div>

    <div class="div-input">
      <Input v-model="valueInput" @keydown.enter="createTodo" class="input" />
    </div>

    <div class="todo-list">
      <Todo
        :todo="todo"
        v-for="todo in todoList"
        :key="todo.name"
        v-on:removed="removed"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Input from "./components/Input.vue";
import Progress from "./components/Progress.vue";
import Todo from "./components/Todo.vue";
import { TodoInterface } from "./types/todo";

import Vue from "vue";

export default Vue.extend({
  name: "app" as string,
  components: {
    Input,
    Progress,
    Todo
  },
  data() {
    return {
      valueInput: "" as string,
      todoList: [] as Array<TodoInterface>,
      percent: 0
    };
  },
  methods: {
    createTodo() {
      if (this.isRegistred()) {
        alert("Tarefá já cadastrada");
        return;
      }

      this.todoList.push({
        name: this.valueInput,
        finished: false
      });

      this.valueInput = "";
    },
    isRegistred(): boolean {
      let isRegitred = this.todoList.map((i: TodoInterface) =>
        i.name === this.valueInput ? true : false
      );
      return isRegitred.includes(true);
    },

    removed(todo: TodoInterface): void {
      let newArray = this.todoList.filter(t => t.name !== todo.name);
      this.todoList = [...newArray];
    }
  },
  watch: {
    todoList: {
      handler(val: Array<Object>): void {
        let completed;
        let arraySize;
        arraySize = val.length;
        completed = val.filter(i => i.finished === true);

        this.percent = (100 * completed.length) / arraySize;
      },
      deep: true
    }
  }
});
</script>

<style lang="sass">
*
  font-family: Arial, Helvetica, sans-serif

body
  margin: 0
  padding: 0
  background: #F8EFBA;
  color: #0d0d0d

#app
  display: flex;
  align-content: center
  justify-content: center
  flex-wrap: wrap

  h1
    width: 100%
    text-align: center

  .div-progress
    width: 100%
    display: flex
    align-items: center
    justify-content: center

    .progress-width
      width: 80%

  .div-input
    width: 70%
    display: flex
    align-items: center
    justify-content: center

    .input
      display: inline-block
      margin-top: 15px

  .todo-list
    width: 70%
    display: grid
    grid-template-columns: repeat(4,1fr)
    grid-gap: 2%;
    margin: 15px;
</style>
