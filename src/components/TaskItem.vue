<template>
  <li :class="{ completed: task.completed }">
    <span>{{ task.title }}</span>
    <button @click="toggleCompletion">Toggle</button>
    <button @click="deleteTask">Delete</button>
  </li>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    task: Object,
  },
  emits: ["delete-task", "toggle-completion"],
  setup(props, { emit }) {
    const toggleCompletion = () => {
      emit("toggle-completion", props.task.id);
    };

    const deleteTask = () => {
      emit("delete-task", props.task.id);
    };

    return { toggleCompletion, deleteTask };
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin: 5px 0;
  background-color: #f0f0f0;
  border-radius: 5px;
}

button {
  margin-left: 10px;
}
</style>
