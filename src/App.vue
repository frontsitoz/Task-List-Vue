<template>
  <div id="app" class="app-container">
    <h1>Task Manager</h1>
    <AddTask @add-task="addTask" />
    <TaskList
      :tasks="tasks"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-completion="toggleCompletion"
    />
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue";
import AddTask from "./components/AddTask.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    AddTask,
    TaskList,
  },

  setup() {
    const tasks = ref([
      { id: 1, title: "Learn Vue.js", completed: false },
      {
        id: 2,
        title: "Build a task manager",
        completed: false,
      },
    ]);

    const addTask = (newTask) => {
      tasks.value.push({
        id: Date.now(),
        title: newTask,
        completed: false,
      });
    };
    const deleteTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id !== taskId);
    };
    const toggleCompletion = (taskId) => {
      const task = tasks.value.find((task) => task.id === taskId);
      if (task) {
        task.completed = !task.completed;

        return {
          tasks,
          addTask,
          deleteTask,
          toggleCompletion,
        };
      }
    };
  },
};
</script>

<style scoped>
#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: "Lato", sans-serif;
  color: #333;
}
h1 {
  text-align: center;
}
</style>
