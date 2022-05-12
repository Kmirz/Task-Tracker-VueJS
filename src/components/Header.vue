<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @button-click="$emit('add-task')" text="Add Task" color="green" />
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
