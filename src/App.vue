<template>
  <Toast :messageStyle="messageStyle" :message="message" />
  <div class="container">
    <Header
      @toggle-show-task="toggleShowAddTask"
      :showAddTasks="showAddTasks"
      title="Task Tracker"
    />
    <AddTask
      v-if="showAddTasks"
      @addedNewTask="addNewTask"
      @incompleteEntry="displayIncompleteMessage"
    />
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
import Toast from "./components/Toast.vue";
import * as bootstrap from "bootstrap";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
    Toast,
  },
  methods: {
    toggleShowAddTask() {
      this.showAddTasks = !this.showAddTasks;
    },
    deleteTask(event, apples) {
      console.log(apples);
      console.log("Delete clicked for ID", event);

      this.tasks = this.tasks.filter((task) => task.id !== event);

      let toastMessage = document.querySelector("#liveToast");
      this.messageStyle = "bg-danger";

      this.message = `Task has been deleted!`;

      let toast = new bootstrap.Toast(toastMessage);
      console.log(toast);
      toast.show();
    },
    toggleAlert(id) {
      console.log("toggle Alert", id);

      const index = this.tasks.findIndex((task) => task.id === id);

      this.tasks[index].reminder = !this.tasks[index].reminder;
    },
    addNewTask(task) {
      this.tasks.unshift(task);

      let toastMessage = document.querySelector("#liveToast");

      this.messageStyle = "bg-success";

      this.message = `New Task of '${this.tasks[0].text}' has been added!`;

      let toast = new bootstrap.Toast(toastMessage);

      toast.show();
    },
    displayIncompleteMessage() {
      let toastMessage = document.querySelector("#liveToast");

      this.messageStyle = "bg-warning";

      this.message = `Please enter all required information to submit`;

      let toast = new bootstrap.Toast(toastMessage);

      toast.show();
    },
  },
  data() {
    return {
      tasks: Array,
      showAddTasks: false,
      messageStyle: "bg-danger",
      message: "",
    };
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctors appointment",
        day: "March 2nd",
        reminder: true,
      },
      {
        id: 2,
        text: "Buy lemons",
        day: "March 22nd",
        reminder: false,
      },
      {
        id: 3,
        text: "Go to the dentist",
        day: "May 5th",
        reminder: true,
      },
      {
        id: 4,
        text: "Parent teacher interview",
        day: "April 1st",
        reminder: true,
      },
      {
        id: 5,
        text: "Buy Larry new game",
        day: "July 1st",
        reminder: true,
      },
      {
        id: 5,
        text: "Do more coding",
        day: "Jan 1st",
        reminder: false,
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
  color: white;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
