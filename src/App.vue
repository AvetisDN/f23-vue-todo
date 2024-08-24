<script setup>
import { ref } from "vue";
import { SunIcon, MoonIcon } from "@heroicons/vue/24/solid";
let appTitle = "ЧёСделать";
const darkMode = ref(false);
const todos = ref([
  {
    id: 0,
    name: "Поспать",
    completed: true,
  },
  {
    id: 1,
    name: "Проснуться",
    completed: true,
  },
  {
    id: 2,
    name: "Позавтракать",
    completed: true,
  },
  {
    id: 3,
    name: "Отобедать",
    completed: false,
  },
  {
    id: 4,
    name: "Поужинать",
    completed: false,
  },
]);
const newTodo = ref("");

function addTodo() {
  const todoItem = {
    id: todos.value.length + 1,
    name: newTodo.value,
    completed: false,
  };
  todos.value.push(todoItem);
  newTodo.value = "";
}

function deleteTodo(id) {
  todos.value = todos.value.filter((todo) => todo.id != id);
}

function toggleTodo(id) {
  todos.value = todos.value.map((todo) => {
    if (todo.id == id) {
      todo.completed = !todo.completed;
    }
    return todo;
  });
}
</script>

<template>
  <div :class="{ dark: darkMode }">
    <div
      class="w-full min-h-screen bg-zinc-200 dark:bg-zinc-950 text-zinc-700 dark:text-zinc-300 grid place-items-center p-4"
    >
      <button
        class="fixed top-4 right-4 w-10 h-10 rounded-full bg-zinc-50 dark:bg-zinc-800 shadow-lg flex items-center justify-center"
        @click="darkMode = !darkMode"
      >
        <SunIcon v-show="!darkMode" class="size-8" />
        <MoonIcon v-show="darkMode" class="size-6" />
      </button>
      <div
        class="bg-zinc-100 dark:bg-zinc-900 p-5 rounded-xl shadow-xl flex flex-col gap-5 w-full max-w-md"
      >
        <!-- Title -->
        <h1
          class="text-blue-500 font-extrabold text-3xl text-center tracking-wide"
        >
          {{ appTitle }}
        </h1>
        <!-- Add form -->
        <form class="flex gap-4" @submit.prevent="addTodo">
          <input
            v-model="newTodo"
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
        <!-- Empty List -->
        <div
          v-if="!todos.length"
          class="grid place-items-center text-2xl font-bold opacity-30 py-10"
        >
          <p>Пока ничё...</p>
        </div>
        <!-- Todo list -->
        <ul v-else class="flex flex-col gap-2 py-2">
          <!-- Todo item -->
          <li
            class="flex items-center justify-between p-3 bg-zinc-50 rounded-md dark:bg-zinc-800 shadow-sm"
            v-for="todo in todos"
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
                @change="toggleTodo(todo.id)"
              />
              <button
                class="w-6 h-6 bg-red-500 text-white text-xl leading-none font-bold"
                @click="deleteTodo(todo.id)"
              >
                &times;
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
