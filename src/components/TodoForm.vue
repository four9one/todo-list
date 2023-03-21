<script lang="ts" setup>
import { ref } from "vue"

const newTodoContent = ref("")

const emit = defineEmits(["submitTodo"])

const addTodo = () => {
  emit("submitTodo", newTodoContent.value)
  newTodoContent.value = ""
}
</script>

<template>
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
</template>

<style>
@import "bulma/css/bulma.min.css";
</style>
