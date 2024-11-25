<!-- TodoApp.vue -->
<script setup>
import { ref, onMounted } from "vue";
import TaskInput from "./Taskinput.vue";
import TaskList from "./TaskList.vue";

const tasks = ref([]);

onMounted(() => {
  const savedTasks = localStorage.getItem("tasks");
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks);
  }
});

const updatedLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};

// Add task
const addTask = (newTask) => {
  tasks.value.push({ text: newTask, completed: false });
  updatedLocalStorage();
};

// Delete task
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
  updatedLocalStorage();
};

const editTask = (index, updatedTask) => {
  tasks.value[index].text = updatedTask;
  updatedLocalStorage();
};

const toggleTaskStatus = (index) => {
  tasks.value[index].completed = !tasks.value[index].completed;
  updatedLocalStorage();
};
</script>

<template>
  <div class="parent-container">
    <div class="todo-container">
      <h1>To-Do List</h1>

      <!-- Input Field Component -->
      <TaskInput @add-task="addTask" />

      <!-- Task List Component -->
      <TaskList
        :tasks="tasks"
        @delete-task="deleteTask"
        @edit-task="editTask"
        @toggle-task-status="toggleTaskStatus"
      />
    </div>
  </div>
</template>

<style scoped>
.parent-container {
  display: flex;
  justify-content: center; /* Horizontally center */
  align-items: center; /* Vertically center */
  /* height: 100vh; Full viewport height */
}

.todo-container {
  text-align: center;
}
</style>
