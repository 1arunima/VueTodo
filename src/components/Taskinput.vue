<!-- TaskInput.vue -->
<template>
  <div class="task-input">
    <input v-model="taskInput" @keyup.enter="addTask" placeholder="Add a new task" multiple required />
    <button @click="addTask"><IconCirclePlus/></button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { IconCirclePlus } from "@tabler/icons-vue";

const taskInput = ref("");
const emit = defineEmits(["add-task"]);

const addTask = () => {
  if (taskInput.value.trim() !== "") {
    emit("add-task", taskInput.value.trim());
    taskInput.value = ""; // Clear the input field
  }
};
</script>

<style scoped>
.task-input {
  display: flex;
  gap: 10px;
}
button {
  background-color:rgb(54, 194, 54);
  padding: 5px 10px;
  width: 30%;
  cursor: pointer;
  font-size: 15px;
  border-radius: 5%;
}

task-list{
  display:flex;
}
</style>
