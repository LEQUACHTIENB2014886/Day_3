<template>
  <nav class="nav-container">
    <form @submit="addItem">
      <input
        type="text"
        placeholder="Thêm công việc mới của bạn !"
        v-model="title"
        @input="check"
      />
      <input type="submit" value="Thêm" class="add-btn" />
    </form>
  </nav>
</template>

<script setup>
import { ref } from "vue";
import { defineEmits } from "vue";
import { v4 as uuidv4 } from "uuid";

const title = ref("");

const check = () => {
  console.log(title.value);
};

const emit = defineEmits("add-todo");

const addItem = (event) => {
  event.preventDefault();

  const newItem = {
    id: uuidv4(),
    title: title.value,
    completed: false,
  };
  emit("add-todo", newItem);
  title.value = "";
};
</script>

<style scoped>
.nav-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

form {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 500px;
  padding: 10px;
  box-sizing: border-box;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
  font-size: 14px;
  width: 100%;
  box-sizing: border-box;
}

input[type="submit"] {
  flex: 2;
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
}
</style>