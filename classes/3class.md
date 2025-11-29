# 👨‍🏫 Capítulo 3/12: Estado e Reatividade (`data` e `computed`)

## 📘 Assuntos Principais

1. Revisão do Estado Reativo (`data()`);
2. Introdução às **Propriedades Computadas (`computed`)**;
3. **Melhores Práticas:** Diferença entre `computed` e `methods`;
4. Exercício: Contagem Reativa de Tarefas Pendentes.

---

## 1. 🧠 Introdução: Reatividade em Profundidade (10 min)

No Vue, o objeto retornado pela função `data()` em um componente se torna o **estado reativo** desse componente.

> 🧩 Quando você altera uma propriedade em `this.propriedade`, o Vue detecta a mudança e automaticamente re-renderiza o DOM — ou seja, a parte da interface que depende dessa propriedade.

Agora, imagine que precisamos calcular o número de tarefas que **não estão concluídas**.
Poderíamos fazer isso em um `method`, mas a melhor prática é usar uma **Propriedade Computada (`computed`)**.

---

## 2. ⚙️ Propriedades Computadas (`computed`) (15 min)

Uma **propriedade computada** é como uma propriedade de dados, mas seu valor é o **resultado de uma função**.

### 🔹 Três Regras de Ouro

1. **Cache:** O resultado de uma `computed` é **armazenado em cache** e só é reavaliado quando _alguma dependência reativa_ usada dentro dela muda (ex: `data` ou `props`).
2. **Performance:** É mais eficiente que um `method`, pois o método é executado **em toda re-renderização**, mesmo se nada tiver mudado.
3. **Função de Leitura:** Deve ser usada para **retornar um valor**, não para executar efeitos colaterais (como chamar APIs ou alterar estado).

---

## 3. 🧩 Exercício: Contagem de Tarefas Pendentes (20 min)

Vamos implementar uma propriedade computada no componente **pai** (`Home.vue`) para exibir a contagem de tarefas pendentes.

---

### 🪜 Passo 1: Criar a Propriedade Computada (`Home.vue`)

No arquivo `src/views/Home.vue`, adicione o bloco `computed` logo abaixo do `data()`:

```vue
<!-- src/views/Home.vue -->
<script>
import TaskItem from "@/components/TaskItem.vue";

export default {
  name: "Home",
  components: {
    TaskItem,
  },
  data() {
    return {
      // (array de tarefas do capítulo anterior)
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
  // Início do bloco computed
  computed: {
    // 1. O nome da função será o nome da nossa propriedade
    tarefasPendentes() {
      // 2. Filtra apenas as tarefas não concluídas
      const pendentes = this.tarefas.filter((t) => !t.concluida);
      // 3. Retorna o total de pendentes
      return pendentes.length;
    },

    // Exemplo de propriedade computada extra
    totalTarefas() {
      return this.tarefas.length;
    },
  },
};
</script>
```

---

### 🪜 Passo 2: Exibir a Contagem no Template

Agora podemos acessar `tarefasPendentes` e `totalTarefas` diretamente no `<template>`.

```vue
<!-- src/views/Home.vue -->
<template>
  <div class="home">
    <h1>Minhas Tarefas</h1>

    <p class="status">
      Você tem
      <strong>{{ tarefasPendentes }}</strong>
      tarefas pendentes de um total de
      {{ totalTarefas }}.
    </p>

    <TaskItem v-for="t in tarefas" :key="t.id" :tarefa="t" />
  </div>
</template>
```

---

### 🧪 Passo 3: Teste de Reatividade (Melhor Prática)

1. Execute o projeto com `npm run serve`.
   → Você deve ver: **"Você tem 2 tarefas pendentes de um total de 3."**

2. No `data()` do `Home.vue`, mude a tarefa 3 para concluída:

   ```js
   { id: 3, titulo: 'Estudar Vuex (Futuro Cap. 7)', concluida: true }
   ```

3. Salve o arquivo.
   → A mensagem deve atualizar automaticamente para:
   **"Você tem 1 tarefa pendente de um total de 3."**

Isso mostra que `tarefasPendentes` detectou a mudança e reavaliou seu resultado **sem precisarmos chamar nada manualmente**.

---

## 4. ⚖️ Bônus: `computed` vs `methods` (10 min)

Essa é uma dúvida muito comum no Vue.

| Característica    | `computed`                                             | `methods`                                                  |
| ----------------- | ------------------------------------------------------ | ---------------------------------------------------------- |
| **Cache**         | ✅ Sim — reavalia apenas quando dependências mudam     | ❌ Não — executa sempre que o componente renderiza         |
| **Uso Principal** | Derivar estado existente (filtrar, formatar, calcular) | Lidar com eventos (cliques, submissões, lógica sem estado) |
| **Acesso**        | Como uma propriedade: `this.meuComputado`              | Como função: `this.meuMetodo()`                            |

> 🧭 **Regra simples:**
> Se você precisa de um valor **reativo derivado** de outros dados → use `computed`.
> Se precisa **executar uma ação**, use `methods`.

---

## 5. 🚀 Preparação para o Próximo Módulo (5 min)

O projeto está funcional, mas ainda simples visualmente.
No **Módulo II**, vamos transformá-lo em uma aplicação profissional com **Vuetify** e **Vue Router**.

- **Próxima Aula:** Configuração do Vuetify e criação do Layout Básico.

---

## 💡 Dica do Dia da Jessie

> ✨ **`computed` ≠ `watch`**
> Embora ambos reajam a mudanças, **usamos `computed` para _retornar um valor_** e **`watch` para _executar uma ação_**.
>
> 🔹 Exemplo:
>
> ```js
> computed: {
>   tarefasPendentes() {
>     return this.tarefas.filter(t => !t.concluida).length;
>   }
> },
>
> watch: {
>   tarefasPendentes(novoValor) {
>     console.log(`Agora você tem ${novoValor} tarefas pendentes!`);
>   }
> }
> ```
>
> 🧠 **Resumo rápido:**
>
> - `computed` → pensa;
> - `watch` → reage.

---

### ✅ Fim da Aula 3

Agora você domina o essencial da **reatividade no Vue.js** — parabéns! 💪

Assinado com carinho,
**– Jessie Moura** 💚
