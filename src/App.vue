<template>
  <div
    class="min-h-screen bg-gradient-to-br from-pink-200 via-purple-300 to-yellow-100 flex items-center justify-center px-4"
  >
    <div class="bg-white shadow-xl rounded-2xl p-6 w-full max-w-md">
      <h1 class="text-2xl font-bold text-center text-purple-700 mb-4">To Do</h1>

      <form @submit.prevent="addTodo" class="flex items-center gap-2">
        <input
          v-model="newTodo"
          type="text"
          placeholder="What will you do today?"
          class="flex-grow p-2 rounded-xl border border-purple-300 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
        <button
          type="submit"
          class="bg-purple-500 hover:bg-purple-600 text-white px-4 py-2 rounded-xl transition duration-300"
        >
          Add
        </button>
      </form>

      <transition-group name="list" tag="ul" class="mt-6 space-y-2">
        <li
          v-for="(todo, index) in todos"
          :key="todo.id"
          class="flex justify-between items-center bg-purple-50 border border-purple-200 p-3 rounded-xl shadow-sm"
        >
          <span class="text-gray-800">{{ todo.text }}</span>
          <button @click="removeTodo(index)" class="text-sm text-red-500 hover:text-red-600 transition">✕</button>
        </li>
      </transition-group>

      <p v-if="todos.length === 0" class="text-center text-purple-500 mt-6">
        You have nothing yet. Let’s get started! 🚀
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('');
const todos = ref([]);

const addTodo = () => {
  if (newTodo.value.trim() === '') return;
  todos.value.push({
    id: Date.now(),
    text: newTodo.value.trim(),
  });
  newTodo.value = '';
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};
</script>

<style>
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}
.list-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
.list-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
