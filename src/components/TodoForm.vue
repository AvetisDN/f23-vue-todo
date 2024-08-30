<script setup>
defineProps(["newTodo"]);
defineEmits(["handle-add-todo"]);
const model = defineModel();
</script>

<template>
  <!-- Add form -->
  <form class="flex gap-4" @submit.prevent="$emit('handle-add-todo')">
    <input
      v-model="model"
      type="text"
      placeholder="Новый чёСделать..."
      class="flex-grow bg-zinc-100 dark:bg-zinc-900 p-4 rounded-md border-2 border-zinc-200 dark:border-zinc-800 outline-none transition-all focus:border-blue-400 focus:dark:border-blue-600"
    />
    <button
      :disabled="newTodo.length < 3"
      type="submit"
      class="p-4 px-5 bg-blue-500 text-zinc-50 rounded-md font-semibold disabled:opacity-30 disabled:pointer-events-none"
    >
      Ну Чё
    </button>
  </form>
</template>
