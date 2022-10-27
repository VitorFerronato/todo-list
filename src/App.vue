<template>
  <div id="app">
    <h1>Tarefas</h1>
    <add-task @taskAdded="addTask" />

    <taskGrid :tasks="tasks" />
  </div>
</template>

<script>
import AddTask from "./components/add-task.vue";
import taskGrid from "./components/task-grid.vue";
export default {
  components: {
    taskGrid,
    AddTask,
  },
  data() {
    return {
      tasks: [
        { name: "Lavar louça", pending: false },
        { name: "Comprar roupa", pending: true },
      ],
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
