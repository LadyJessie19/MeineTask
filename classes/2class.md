# 👨‍🏫 Capítulo 2/12: Componentização e Propriedades (Props)

## 📚 Assuntos Principais

1. O Conceito de **Single File Component (SFC)**
2. Criando o nosso primeiro componente reutilizável (`<TaskItem/>`)
3. Comunicação **Pai-Filho** usando **Props**
4. **Melhores Práticas:** Validação de Props e Estrutura de Pastas

---

## 🧩 1. Introdução: O Poder dos Componentes (10 min)

No **Vue.js**, uma aplicação é uma **árvore de componentes**.
Um **Single File Component (SFC)** é a forma padrão de criar componentes no Vue e é identificado pelo arquivo com extensão `.vue`.

Um SFC é dividido em **três blocos principais**:

1. **`<template>`** – Estrutura HTML e diretivas do Vue
2. **`<script>`** – Lógica JavaScript (dados, métodos, ciclo de vida)
3. **`<style>`** – CSS específico do componente (pode ter `scoped` para isolamento)

🎯 **Objetivo da Aula:** Criar o componente responsável por _exibir uma única tarefa_ na nossa lista — o `<TaskItem/>`.

---

## 🛠️ 2. Exercício: Criação do Componente `<TaskItem/>` (15 min)

### **Passo 1: Criar a Estrutura de Pastas**

Na pasta `src`, criaremos uma estrutura limpa para organizar os componentes:

1. Crie a pasta: `src/components/`
2. Dentro dela, crie o arquivo: `TaskItem.vue`

---

### **Passo 2: Definir a Estrutura Básica do SFC**

Dentro de `TaskItem.vue`, insira o esqueleto do componente:

```vue
<template>
  <div class="task-item"></div>
</template>

<script>
export default {
  // Melhores Práticas: Nomeclatura PascalCase
  name: "TaskItem",
  data() {
    return {}; // Este componente será "burro" e não terá estado próprio por enquanto.
  },
};
</script>

<style scoped>
/* O atributo 'scoped' garante que o CSS só afete este componente */
.task-item {
  padding: 10px;
  border-bottom: 1px solid #eee;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
```

---

## 🔗 3. Propriedades (Props): Comunicação Pai-Filho (20 min)

Um componente é **reutilizável** quando ele recebe dados de fora para se renderizar.
É aqui que entram as **Props (Propriedades)**.

Props são **dados personalizados** que um componente **filho** espera receber do **pai**.
Elas são de **fluxo unidirecional** → o pai **envia**, o filho **lê**.

---

### **Passo 3: Definir as Props no Componente Filho (`TaskItem.vue`)**

Nossa tarefa será um objeto com a seguinte estrutura:

```js
{ id: 1, titulo: 'Estudar Vuex', concluida: false }
```

Atualize o `<script>` do `TaskItem.vue`:

```vue
<script>
export default {
  name: "TaskItem",
  // 1. Definição do objeto props
  props: {
    // 2. Criamos a prop 'tarefa' que deve ser um Objeto
    tarefa: {
      type: Object, // Melhores Práticas: Validação de Tipo
      required: true, // Garante que a prop será passada
      // 3. Opcional: Validador customizado para garantir a estrutura mínima
      validator(value) {
        return ["id", "titulo", "concluida"].every((key) => key in value);
      },
    },
  },
};
</script>
```

---

### **Passo 4: Usar as Props no Template do Filho (`TaskItem.vue`)**

```vue
<template>
  <div class="task-item" :class="{ concluida: tarefa.concluida }">
    <span
      :style="{ textDecoration: tarefa.concluida ? 'line-through' : 'none' }">
      {{ tarefa.titulo }}
    </span>
    <button>X</button>
  </div>
</template>

<style scoped>
/* ... (estilos existentes) ... */
.concluida {
  background-color: #f0f0f0;
}
</style>
```

---

## 🏠 4. Exercício: Renderizando o Componente (Pai) (15 min)

O componente **Pai** será o `Home.vue`.
Ele será responsável por gerenciar a lista de tarefas e **passar cada tarefa** para o `<TaskItem/>`.

---

### **Passo 5: Preparar Dados Mockados (Temporário)**

No arquivo `src/views/Home.vue`, adicione o seguinte código:

```vue
<template>
  <div class="home">
    <h1>Minhas Tarefas</h1>
    <TaskItem v-for="t in tarefas" :key="t.id" :tarefa="t" />
  </div>
</template>

<script>
// 1. Importa o componente filho
import TaskItem from "@/components/TaskItem.vue";

export default {
  name: "Home",
  // 2. Registra o componente
  components: { TaskItem },
  data() {
    return {
      // Estado reativo com a lista de tarefas
      tarefas: [
        { id: 1, titulo: "Configurar o ambiente (Cap. 1)", concluida: true },
        {
          id: 2,
          titulo: "Criar o componente TaskItem (Cap. 2)",
          concluida: false,
        },
        { id: 3, titulo: "Estudar Vuex (Futuro Cap. 7)", concluida: false },
      ],
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
```

---

### **Passo 6: Entendendo a Sintaxe (`v-for` e `v-bind`)**

1. `v-for="t in tarefas"` → Itera sobre o array `tarefas`
2. `:key="t.id"` → **Melhor Prática:** ajuda o Vue a rastrear cada item da lista
3. `:tarefa="t"` → Usa `v-bind` para passar a prop `tarefa` ao filho `<TaskItem/>`

---

## ✅ 5. Verificação e Revisão (10 min)

1. **Execute ou Verifique:** Se o servidor (`npm run serve`) ainda estiver rodando, o navegador deve atualizar automaticamente.
2. **Resultado esperado:** Lista das três tarefas renderizadas, com a primeira riscada.
3. **Teste a Reatividade:** Adicione uma nova tarefa no array `tarefas` e salve — a lista deve atualizar instantaneamente.

---

🎉 **Parabéns!**
Você criou um **componente reutilizável** e aplicou a comunicação **Pai-Filho** com **Props**, um dos conceitos mais essenciais do Vue.js.

---

### 🚀 Próximo Capítulo

No **Capítulo 3**, aprenderemos a usar **propriedades computadas (`computed`)** e prepararemos o projeto para receber o **Vuetify**.
