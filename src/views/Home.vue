<template>
  <div class="home">
    <h1>Minhas Tarefas</h1>

    <p class="status">
      Você tem <strong>{{ tarefasPendentes }}</strong> tarefas pendentes de um
      total de {{ totalConcluidas }}.
    </p>

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
  computed: {
    tarefasPendentes() {
      const pendentes = this.tarefas.filter((item) => !item.concluida);
      return pendentes.length;
    },
    totalConcluidas() {
      return this.tarefas.length;
    },
  },
};
</script>

<style scoped>
.home {
  max-width: 600px;
  margin: 0 auto;
}
</style>
