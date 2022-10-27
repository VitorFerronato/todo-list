<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <task
      @taskStateChange="$emit('taskStateChange', index)"
        @taskDeleted="$emit('taskDeleted', index)"
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
      >
      </task>
    </template>
    <p v-else class="no-task">Sua vida está em dia :)</p>
  </div>
</template>

<script>
import task from "./task.vue";
export default {
  components: { task },
  props: {
    tasks: { type: Array, required: true },
  },

  data() {
    return {};
  },
};
</script>

<style >
.task-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 10px;
}

.no-task {
  color: #aaa;
  font-size: 1.7rem;
}
</style>