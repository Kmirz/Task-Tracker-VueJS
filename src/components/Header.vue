<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-if="!showAddTasks"
      @button-click="$emit('toggle-show-task')"
      text="Add Task"
      color="green"
    />
    <Button
      v-if="showAddTasks"
      @button-click="$emit('toggle-show-task')"
      text="Hide Task"
      color="red"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    title: {
      type: String,
    },
    showAddTasks: false,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
