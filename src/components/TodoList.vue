<script setup>
import TodoListItem from "./TodoListItem.vue";

defineProps(["todos", "onDelete", "onToggle"]);
</script>

<template>
  <!-- Todo list -->
  <ul class="flex flex-col gap-2 py-2">
    <TodoListItem
      v-for="todo in todos"
      :todo="todo"
      :onDelete="onDelete"
      :onToggle="onToggle"
    />
  </ul>
</template>
