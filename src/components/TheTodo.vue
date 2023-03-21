<script setup>
import TodoForm from "@/components/TodoForm.vue"
import TodoList from "@/components/TodoList.vue"
import { h, ref, defineAsyncComponent } from "vue"
import { v4 as uuidv4 } from "uuid"
// import TodoInfo from "./TodoInfo.vue"

// const TodoInfo = defineAsyncComponent(() => import("@/components/TodoInfo.vue"))
const TodoInfo = defineAsyncComponent({
  loader: () => {
    return new Promise((resolve, reject) => {
      let e = setTimeout(() => {
        resolve(import("@/components/TodoInfo.vue"))
      }, 2000)
    })
  },
  loadingComponent: h("div", { id: "foo", innerHTML: "loading..." }),
  delay: 100,
})

const todos = ref([
  { id: "id1", content: "Klippa gräset", done: false },
  { id: "id2", content: "Handla mat inför veckan", done: false },
])

const showInfo = ref(false)

const submitTodo = (todoContent) => {
  todos.value.unshift({
    id: uuidv4(),
    content: todoContent,
    done: false,
  })
}
const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const toggleDone = (id) => {
  const foundTodo = todos.value.find((todo) => todo.id === id)
  foundTodo.done = !foundTodo.done
}
</script>

<template>
  <div class="badass-todo container content">
    <div class="title has-text-centered">Att göra lista</div>
    <TodoForm @submitTodo="submitTodo" />
    <TodoList
      :todos="todos"
      @toggleDone="toggleDone"
      @deleteTodo="deleteTodo"
    />
    <hr />
    <button class="button" @click="showInfo = true">Show info</button>
    <TodoInfo v-if="showInfo" />
  </div>
</template>

<style>
@import "bulma/css/bulma.min.css";
.badass-todo {
  max-width: 400px;
  width: 400px;
  padding: 20px;
  margin: 0 auto;
}
</style>
