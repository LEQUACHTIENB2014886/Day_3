<template>
  <div>
    <h1>Các công việc</h1>
    <a>
      <AddTodo @add-todo="addTodo" />
      <!-- component con -->
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todoPros="todo"
        @item-completed="markCompleted"
        @delete-item="deleteTodo"
      />
    </a>
  </div>
</template>

<script setup>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
import axios from "axios";
// Tạo mảng todos
const todos = ref([
  // { id: 1, completed: false, title: "HTML" },
  // { id: 2, completed: false, title: "CSS" },
  // { id: 3, completed: false, title: "JavaScript" },
  // { id: 4, completed: false, title: "Vue.js" },
]);

const getAllTodos = async () => {
  try {
    const res = await axios.get(
      "https://jsonplaceholder.typicode.com/todos?_limit=5"
    );
    console.log(res.data);
    todos.value = res.data;
  } catch (error) {
    console.log(error);
  }
};

// Hàm đánh dấu công việc hoàn thành
const markCompleted = (id) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id == id) todo.completed = !todo.completed;
    return todo;
  });
};

// Hàm xóa công việc
const deleteTodo = async (id) => {
  try {
    await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
    todos.value = todos.value.filter((todo) => todo.id !== id);
  } catch (error) {
    console.log(error);
  }
};

const addTodo = async (newTodo) => {
  try {
    const res = await axios.post(
      `https://jsonplaceholder.typicode.com/todos/`,
      newTodo
    );
    todos.value.push(res.data);
  } catch (error) {
    console.log(error);
  }
};
getAllTodos();
</script>
  
<style scoped>
h1 {
  color: rgb(98, 226, 240);
  font-weight: blod;
  text-align: center;
  margin-top: 30px;
  text-shadow: 1px 1px 1px rgb(17, 133, 159);
}
</style>