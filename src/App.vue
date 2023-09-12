<template>
  <div id="app">
    <div class="center-content">
      <h1>Gerenciador de Tarefas</h1>
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Adicionar uma tarefa"
      />
      <div v-for="task in tasks" :key="task.id">
        <TaskItem :task="task" @toggle="toggleTask" @delete="deleteTask" />
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./components/Task.vue";

export default {
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: "",
      tasks: [],
      taskIdCounter: 1,
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === "") return;
      this.tasks.push({
        id: this.taskIdCounter++,
        text: this.newTask,
        completed: false,
      });
      this.newTask = "";
    },
    toggleTask(taskId) {
      const task = this.tasks.find((t) => t.id === taskId);
      if (task) {
        task.completed = !task.completed;
      }
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
  },
};
</script>

<style>
.center-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  height: 100vh;
  text-align: center;
  background-image: url("./img/img.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  color: white;
}
</style>
