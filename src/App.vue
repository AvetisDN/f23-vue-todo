<script setup>
import { ref } from "vue";
import { SunIcon, MoonIcon } from "@heroicons/vue/24/solid";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";
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
        <TodoForm
          :new-todo="newTodo"
          @handle-add-todo="addTodo"
          v-model="newTodo"
        />
        <!-- Empty List -->
        <div
          v-if="!todos.length"
          class="grid place-items-center text-2xl font-bold opacity-30 py-10"
        >
          <p>Пока ничё...</p>
        </div>
        <TodoList
          v-else
          :todos="todos"
          :onDelete="deleteTodo"
          :onToggle="toggleTodo"
        />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
