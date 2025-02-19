<script setup lang="ts">
import { ref } from "vue";

interface TodoItem {
  text: string;
  done: boolean;
}
const todoInput = ref(""); //ใช้เก็บค่า input
const todoList = ref<TodoItem[]>([]); // รายการ Todo

function addList() {
  if (todoInput.value.trim()) {
    //ป้องกันการเพิ่มค่าว่าง

    todoList.value.push({
      text: todoInput.value,
      done: false,
    });
    todoInput.value = ""; // รีเซ็ต imput
  }
}

function deleteList(index: number) {
  todoList.value.splice(index, 1);
}
</script>

<template>
  <div class="container mx-auto my-5">
    <div class="rounded shadow-lg p-4 w-100 mx-auto">
      <h1 class="text-3xl font-bold text-center mb-5 text-blue-600 dark:text-sky-400">Todo APP</h1>
      <ul class="mb-3">
        <li v-for="(todo, index) in todoList" :key="index" class="flex-warp space-x-2">
          <input v-model="todo.done" type="checkbox" />
          <span class="grow w-100" :class="{'line-through' : todo.done}">{{ todo.text }}</span>
          <a href="#" class="underline text-blue-500" @click="deleteList(index)">ลบ</a>
        </li>
      </ul>
      <form @submit.prevent="addList" class="flex">
        <input class="px-2 py-1 border rounded focus:outline-blue-500" 
        v-model="todoInput" type="text" placeholder="เพิ่มรายการใหม่" />
        <button class="bg-blue-500 px-3 py-1 ml-10 rounded text-white" type="submit">เพิ่มรายการ</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
