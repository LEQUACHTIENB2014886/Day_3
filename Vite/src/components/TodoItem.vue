<template>
  <nav :class="['edit', todoPros.completed ? ' is-completed' : '']">
    <div class="checkbox">
      <input
        type="checkbox"
        :checked="todoPros.completed"
        @change="markItemCompleted"
      />
    </div>
    <div class="type">{{ todoPros.type }}</div>
    <div class="title">{{ todoPros.title }}</div>
    <div class="del-btn"><button @click="deleteItem">Delete</button></div>
  </nav>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

// Định nghĩa props
const props2 = defineProps({
  todoPros: {
    type: Object,
    required: true,
  },
});
// console.log(props2.todoPros);
// Định nghĩa các sự kiện emit
const emit = defineEmits(["item-completed", "delete-item"]);

// Hàm thông báo công việc đã hoàn thành
const markItemCompleted = () => {
  emit("item-completed", props2.todoPros.id); // Gửi sự kiện lên parent với id của công việc
};

// Hàm thông báo xóa công việc
const deleteItem = () => {
  emit("delete-item", props2.todoPros.id); // Gửi sự kiện xóa lên parent
};
</script>

<style scoped>
.edit {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin: 10px auto;
  max-width: 400px;
  background: #ffffff;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.title {
  margin-left: 20px;
}
.del-btn {
  margin-left: auto;
}

.is-completed {
  text-decoration: line-through;
}
</style>