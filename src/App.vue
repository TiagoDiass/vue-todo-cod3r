<template>
  <div id="app">
    <h1>Tarefas</h1>

    <TaskProgress :progress="progress" />

    <NewTask @taskAdded="addTask($event)" />

    <TaskGrid
      :tasks="tasks"
      @taskStateChanged="toggleTaskState($event)"
      @taskDeleted="deleteTask($event)"
    />
  </div>
</template>

<script>
import TaskProgress from "./components/TaskProgress.vue";
import NewTask from "./components/NewTask.vue";
import TaskGrid from "./components/TaskGrid.vue";

function newTask(name, pending = true) {
  return {
    name,
    pending
  };
}

export default {
  components: { TaskGrid, NewTask, TaskProgress },

  data: () => ({
    tasks: [
      newTask("Lavar a louça", false),
      newTask("Comprar blusa"),
      newTask("Fazer café", false)
    ]
  }),

  computed: {
    progress() {
      const doneTasks = this.tasks.filter(task => !task.pending);
      return parseInt((doneTasks.length / this.tasks.length) * 100);
    }
  },

  methods: {
    addTask(task) {
      const sameName = t => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;

      if (reallyNew) this.tasks.push(newTask(task.name));
    },

    deleteTask(taskIndex) {
      this.tasks.splice(taskIndex, 1);
    },

    toggleTaskState(index) {
      this.tasks[index].pending = !this.tasks[index].pending;
    }
  }
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
