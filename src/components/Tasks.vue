<template>
  <div class="task-container">
    <div :key="task.id" v-for="task in tasks">
      <task
        @delete-clicked="$emit('delete-clicked', task.id)"
        @task-clicked="$emit('task-clicked', task.id)"
        :task="task"
      />
    </div>
  </div>
</template>

<script>
import Task from "./Task.vue";

export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits: ["delete-clicked", "task-clicked"],
};
</script>

<style scoped>
.task-container {
  max-height: 200px;
  overflow-y: auto;
}
</style>