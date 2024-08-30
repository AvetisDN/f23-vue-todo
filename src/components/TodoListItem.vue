<script setup>
defineProps(["todo", "onDelete", "onToggle"]);
</script>

<template>
  <!-- Todo item -->
  <li
    class="flex items-center justify-between p-3 bg-zinc-50 rounded-md dark:bg-zinc-800 shadow-sm"
    :class="{ completed: todo.completed }"
  >
    <h4 class="text-xl font-semibold">
      {{ todo.name }}
    </h4>
    <div class="flex items-center gap-4">
      <input
        type="checkbox"
        class="w-6 h-6"
        :checked="todo.completed"
        @change="onToggle(todo.id)"
      />
      <button
        class="w-6 h-6 bg-red-500 text-white text-xl leading-none font-bold"
        @click="onDelete(todo.id)"
      >
        &times;
      </button>
    </div>
  </li>
</template>
