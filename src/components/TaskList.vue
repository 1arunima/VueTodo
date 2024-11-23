<template>
  <div>
    <!-- Tabs for Task View -->
    <div class="tabs">
      <button
        :class="{ active: activeTab === 'all' }"
        @click="activeTab = 'all'"
      >
        All Tasks
      </button>
      <button
        :class="{ active: activeTab === 'active' }"
        @click="activeTab = 'active'"
      >
        Active Tasks
      </button>
      <button
        :class="{ active: activeTab === 'completed' }"
        @click="activeTab = 'completed'"
      >
        Completed Tasks
      </button>
    </div>

    <!-- Task List -->
    <ul>
      <li
        v-for="(taskItem, index) in filteredTasks"
        :key="index"
      >
        <!-- Editing mode -->
        <div v-if="editingIndex === index" class="task-container">
          <input
            type="text"
            v-model="updatedTask"
            placeholder="Edit your task"
          />
          <div class="button-group">
            <button class="btn-update" @click="updateTask(index)">
              <IconCircleCheck /> Update
            </button>
            <button class="btn-cancel" @click="cancelEdit">
              <IconCircleX /> Cancel
            </button>
          </div>
        </div>

        <!-- Default mode -->
        <div v-else class="task-container">
          <p :class="{ 'task-completed': taskItem.completed }" class="task-text">
            {{ taskItem.text }}
          </p>
          <div class="button-group">
            <!-- Conditionally show Edit and Remove buttons only in Active Tasks -->
            <template v-if="activeTab === 'active'">
              <button class="btn-edit" @click="startEdit(index, taskItem.text)">
                <IconEdit class="icon-edit" /> Edit
              </button>
              <button class="btn-remove" @click="deleteTask(index)">
                <IconTrashX class="icon-remove" /> Remove
              </button>
            </template>
            <!-- Toggle completion -->
            <button
              :class="taskItem.completed ? 'btn-active' : 'btn-complete'"
              @click="toggleComplete(index)"
            >
              <IconCircleCheck v-if="!taskItem.completed" />
              <IconCircleX v-else />
              {{ taskItem.completed ? "Active" : "Completed" }}
            </button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { IconEdit, IconTrashX, IconCircleCheck, IconCircleX } from "@tabler/icons-vue";

const props = defineProps({
  tasks: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["delete-task", "edit-task", "toggle-task-status"]);

const editingIndex = ref(null);
const updatedTask = ref("");

const activeTab = ref("all");

// Handle delete task
const deleteTask = (index) => {
  emit("delete-task", index);
};

// Start editing a task
const startEdit = (index, taskText) => {
  editingIndex.value = index;
  updatedTask.value = taskText;
};

// Update the task and exit editing mode
const updateTask = (index) => {
  if (updatedTask.value.trim() !== "") {
    emit("edit-task", index, updatedTask.value);
  }
  cancelEdit();
};

// Cancel edit
const cancelEdit = () => {
  editingIndex.value = null;
  updatedTask.value = "";
};

// Toggle task completion
const toggleComplete = (index) => {
  emit("toggle-task-status", index);
};

// Filter tasks based on active tab
const filteredTasks = computed(() => {
  if (activeTab.value === "active") {
    return props.tasks.filter((task) => !task.completed);                     
  } else if (activeTab.value === "completed") {
    return props.tasks.filter((task) => task.completed);
  }
  return props.tasks;
});
</script>

<style scoped>
/* Tabs Styling */
/* Tabs Styling */
.tabs {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 20px;
  width: 100%;
  max-width: 600px; /* Ensure consistent width */
  margin: 0 auto; /* Center the tabs */
}

.tabs button {
  padding: 6px 5px; /* Increase padding for better alignment */
  font-size: 16px;
  border: none;
  border-radius: 5px;
  background-color: #ddd;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: 100%; /* Make buttons fill the container */
  max-width: 150px; /* Limit the max-width for consistency */
  text-align: center;
}

.tabs button.active {
  background-color: #2196f3;
  color: white;
}

/* Task List Styling */
ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
   /* Ensure consistent width */
  margin: 0 auto; /* Center the task list */
}

li {
  display: flex;
  flex-direction: column;
  background: #f4f4f4;
  padding: 8px;
  border-radius: 8px;
  width: 698px;
  margin: 10px auto;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

/* Task Text Styling */
.task-completed {
  text-decoration: line-through;
  color: gray;
}

/* Other Styles */
.task-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  min-height: 80px;
  margin-bottom: 0;
  width: 100%;
  height: 100%;
}

.task-text {
  margin: 0;
  font-size: 16px;
  font-weight: bold;
  flex-grow: 1;
  text-align: start;
  word-wrap: break-word;
  overflow-wrap: break-word;
  max-width: 80%;
  min-width: 54%;
}

.button-group {
  display: flex;
  gap: 8px; 
  align-items: center; 
}

button {
  display: inline-flex; 
  align-items: center; 
  justify-content: center;
  gap: 4px;
  padding: 5px 10px; 
  font-size: 14px; 
  font-weight: 500;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

button .icon {
  font-size: 16px; 
  vertical-align: middle; 
}

button:hover {
  transform: scale(1.05); 
}

.btn-update {
  background: #45a049;
  color: white;
}

.btn-cancel {
  background: #c92828;
  color: white;
}

.btn-edit {
  background: #2196f3;
  color: white;
}

.btn-remove {
  background: #c92828;
  color: white;
}

.btn-complete {
  background: #45a049;
  color: white;
}

.btn-active {
  background: #2196f3;
  color: white;
}

</style>
