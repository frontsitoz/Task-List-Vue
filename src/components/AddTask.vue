<template>
  <div>
    <input v-model="taskTitle" placeholder="Entertask" @keyup.enter="addTask" />
    <button @click="addTask">Add Task</button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "AddTask",
  emits: ["add-task"],
  setup(_, { emit }) {
    const taskTitle = ref("");

    const addTask = () => {
      if (taskTitle.value.trim()) {
        emit("add-task", taskTitle.value);
        taskTitle.value = ""; //Reset input
      }
    };
    return { taskTitle, addTask };
  },
};
</script>

<style scoped>
input {
  padding: 10px;
  width: 80%;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
}

button {
  padding: 10px;
  width: 80%;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
}
</style>
