<template>
  <div
    id="liveToast"
    class="
      toast
      position-fixed
      top-0
      start-50
      translate-middle-x
      text-white
      bg-success
      border-0
    "
    role="alert"
    aria-live="assertive"
    aria-atomic="true"
    style="position: absolute; width: auto; text-align: center"
  >
    <div class="d-flex">
      <div class="toast-body">A new task has been added!</div>
      <button
        type="button"
        class="btn-close btn-close-white me-2 m-auto"
        data-bs-dismiss="toast"
        aria-label="Close"
      ></button>
    </div>
  </div>

  <div class="container">
    <Header
      @toggle-show-task="toggleShowAddTask"
      :showAddTasks="showAddTasks"
      title="Task Tracker"
    />
    <AddTask v-if="showAddTasks" @addedNewTask="addNewTask" />
    <Tasks
      @delete-clicked="deleteTask($event, 1)"
      @task-clicked="toggleAlert"
      :tasks="tasks"
      :showAddTasks="showAddTasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import * as bootstrap from "bootstrap";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  methods: {
    toggleShowAddTask() {
      this.showAddTasks = !this.showAddTasks;
    },
    deleteTask(event, apples) {
      console.log(apples);
      console.log("Delete clicked for ID", event);
      this.tasks = this.tasks.filter((task) => task.id !== event);
    },
    toggleAlert(id) {
      console.log("toggle Alert", id);

      const index = this.tasks.findIndex((task) => task.id === id);

      this.tasks[index].reminder = !this.tasks[index].reminder;
    },
    addNewTask(task) {
      this.tasks.unshift(task);

      let toastMessage = document.querySelector("#liveToast");

      let toast = new bootstrap.Toast(toastMessage);

      toast.show();
    },
  },
  data() {
    return {
      tasks: Array,
      showAddTasks: false,
    };
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctors Appointment 1",
        day: "March 2nd",
        reminder: "true",
      },
      {
        id: 2,
        text: "Doctors Appointment 2",
        day: "March 2nd",
        reminder: "true",
      },
      {
        id: 3,
        text: "Doctors Appointment 3",
        day: "March 2nd",
        reminder: "true",
      },
    ];
  },
  emits: ["delete-clicked", "task-clicked", "addedNewTask"],
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: green;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
  color: green;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
