<template>
  <div id="app">
    <h1>Tarefas</h1>
    <task-progress :progress="progress" />
    <add-task @taskAdded="addTask" />

    <taskGrid
      @taskStateChange="toggleState"
      @taskDeleted="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import AddTask from "./components/add-task.vue";
import taskGrid from "./components/task-grid.vue";
import taskProgress from "./components/task-progress.vue";
export default {
  components: {
    taskGrid,
    AddTask,
    taskProgress,
  },
  data() {
    return {
      tasks: [],
    };
  },

  methods: {
    addTask(task) {
      const sameName = (t) => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;
      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        });
      }
    },

    deleteTask(i) {
      this.tasks.splice(i, 1);
    },

    toggleState(i) {
      this.tasks[i].pending = !this.tasks[i].pending;
    },
  },

  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter((t) => !t.pending).length;
      return Math.round((done / total) * 100) || 0;
    },
  },

  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },

  created() {
    const json = localStorage.getItem("tasks");
    const array = JSON.parse(json);
    this.tasks = Array.isArray(array) ? array : [];
  },
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
