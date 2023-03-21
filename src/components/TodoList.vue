<script setup lang="ts">
import { ref } from "vue"
import { v4 as uuidv4 } from "uuid"

const emit = defineEmits(["toggleDone", "deleteTodo"])

type TodoType = {
  id: string
  content: string
  done: boolean
}

defineProps<{
  todos: [TodoType]
}>()
</script>

<template>
  <div
    v-for="todo in todos"
    class="card mb-4"
    :class="{ 'has-background-success-light': todo.done }"
    :key="todo.id"
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
              @click="$emit('toggleDone', todo.id)"
            >
              &check;
            </button>
            <button
              @click="$emit('deleteTodo', todo.id)"
              class="button is-danger ml-2"
            >
              &cross;
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import "bulma/css/bulma.min.css";

.line-through {
  text-decoration: line-through;
}
</style>
