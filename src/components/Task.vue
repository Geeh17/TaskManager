<template>
  <div class="task">
    <input type="checkbox" :checked="task.completed" @change="toggleTask" />
    <span :class="{ completed: task.completed }">{{ task.text }}</span>
    <button @click="deleteTask">Deletar</button>
  </div>
</template>

<script>
export default {
  name: 'TaskItem', 
  props: ['task'],
  methods: {
    toggleTask() {
      this.$emit('toggle', this.task.id);
    },
    deleteTask() {
      this.$emit('delete', this.task.id);
    },
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}

</style>
