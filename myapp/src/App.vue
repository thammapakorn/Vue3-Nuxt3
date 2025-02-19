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

function deleteList(index: number){
    todoList.value.splice(index,1)
  }
</script>

<template>
  <div>
    <h1>Todo APP</h1>
    <ul>
      <li v-for="(todo, index) in todoList" :key="index">
        <input v-model="todo.done" type="checkbox" />
        {{ todo.text }}
        <a href="#" @click="deleteList(index)">ลบ</a>
      </li>
    </ul>
    <form @submit.prevent="addList">
      <input v-model="todoInput" type="text" placeholder="เพิ่มรายการใหม่" />
      <button type="submit">เพิ่มรายการ</button>
    </form>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
