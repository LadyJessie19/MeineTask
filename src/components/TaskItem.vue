<template>
  <div class="task-item" :class="{ concluida: tarefa.concluida }">
    <span
      :style="{ textDecoration: tarefa.concluida ? 'line-through' : 'none' }">
      {{ tarefa.titulo }}
    </span>
    <button>X</button>
  </div>
</template>
<script>
export default {
  name: "TaskItem",
  props: {
    tarefa: {
      type: Object,
      required: true,
      validator(value) {
        return ["id", "titulo", "concluida"].every((key) => key in value);
      },
    },
  },
  data() {
    return {};
  },
};
</script>
<style scoped>
.task-item {
  padding: 10px;
  border-bottom: 1px solid #eee;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.concluida {
  background-color: #f0f0f0;
}
</style>
