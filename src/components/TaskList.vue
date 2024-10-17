<template>
  <ul>
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @delete-task="deleteTask"
      @toggle-completion="toggleCompletion"
    />
  </ul>
</template>

<script>
import { defineProps, defineEmits } from "vue";
import TaskItem from "./TaskItem.vue";

export default {
  name: "TaskList",
  components: {
    TaskItem,
  },
  props: {
    tasks: Array,
  },
  setup(props, { emit }) {
    const deleteTask = (taskId) => {
      emit("delete-task", taskId);
    };

    const toggleCompletion = (taskId) => {
      emit("toggle-completion", taskId);
    };

    return { deleteTask, toggleCompletion };
  },
};
</script>
