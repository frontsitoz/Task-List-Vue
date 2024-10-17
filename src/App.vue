<template>
  <div id="app">
    <h1>Task Manager</h1>
    <AddTask @add-task="addTask" />
    <TaskList
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-completion="toggleCompletion"
    />
  </div>
</template>

<script>
import { ref } from "vue";
import TaskList from "./components/TaskList.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    TaskList,
    AddTask,
  },
  setup() {
    const tasks = ref([
      { id: 1, title: "Learn Vue.js", completed: false },
      { id: 2, title: "Build a project", completed: false },
    ]);

    const addTask = (newTask) => {
      tasks.value.push({ id: Date.now(), title: newTask, completed: false });
    };

    const deleteTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id !== taskId);
    };

    const toggleCompletion = (taskId) => {
      const task = tasks.value.find((t) => t.id === taskId);
      if (task) task.completed = !task.completed;
    };

    return { tasks, addTask, deleteTask, toggleCompletion };
  },
};
</script>

<style scoped>
#app {
  max-width: 600px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  padding: 20px;
}

h1 {
  text-align: center;
}
</style>
