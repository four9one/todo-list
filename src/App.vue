<script setup>
import { ref } from "vue"
import { v4 as uuidv4 } from "uuid"

const todos = ref([
  { id: "id1", content: "Klippa gräset", done: false },
  { id: "id2", content: "Handla mat inför veckan", done: false },
])

const newTodoContent = ref("")

const addTodo = () => {
  todos.value.unshift({
    id: uuidv4(),
    content: newTodoContent.value,
    done: false,
  })
  newTodoContent.value = ""
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
  <div class="badass-todo">
    <div class="title has-text-centered">Att göra lista</div>

    <form @submit.prevent="addTodo">
      <div class="field is-grouped mb-5">
        <p class="control is-expanded">
          <input
            class="input"
            type="text"
            placeholder="Add a todo"
            v-model="newTodoContent"
          />
        </p>
        <p class="control">
          <button :disabled="newTodoContent.length < 3" class="button is-info">
            Add
          </button>
        </p>
      </div>
    </form>

    <div
      v-for="todo in todos"
      class="card mb-4"
      :class="{ 'has-background-success-light': todo.done }"
    >
      <div class="card-content">
        <div class="content">
          <div class="columns is-mobile is-vcentered">
            <div
              class="column"
              :class="todo.done ? 'has-text-success line-through' : ''"
            >
              {{ todo.content }}
            </div>
            <div class="column is-5 has-text-right">
              <button
                :class="todo.done ? 'is-success' : 'is-light'"
                class="button"
                @click="toggleDone(todo.id)"
              >
                &check;
              </button>
              <button
                @click="deleteTodo(todo.id)"
                class="button is-danger ml-2"
              >
                &cross;
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import "bulma/css/bulma.min.css";

.badass-todo {
  max-width: 400px;
  padding: 20px;
  margin: 0 auto;
}
.line-through {
  text-decoration: line-through;
}
</style>
