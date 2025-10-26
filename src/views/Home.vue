<template>
  <div class="home">
    <h1>Minhas Tarefas</h1>
    <TaskItem v-for="t in tarefas" :key="t.id" :tarefa="t" />
  </div>
</template>

<script>
import TaskItem from "@/components/TaskItem.vue";
import tasks from "@/data/tasks";

export default {
  name: "Home",
  components: { TaskItem },
  data() {
    return {
      tarefas: tasks,
    };
  },
};
</script>

<style scoped>
.home {
  max-width: 600px;
  margin: 0 auto;
}
</style>
