# 📝 Gerenciador de Tarefas Reativo (Vue.js + Vuex)

Este é o projeto final do curso "Vue.js Full-Stack Básico", com foco em **Vue.js**, **Vuex**, **Vuetify**, **Vue Router** e **Axios**.

## 👨‍🏫 Capítulo 1/12: Introdução ao Vue.js e Setup do Projeto

### 🧩 Assuntos Principais

1. **O que é Vue.js?** (Breve Introdução)
2. **Vue CLI:** A ferramenta essencial para iniciar projetos.
3. **Configuração do Ambiente** (Node.js e Vue CLI).
4. **Estrutura Básica do Projeto** e Limpeza Inicial.
5. **Melhor Prática:** Criando um `README.md` completo.

---

### 📌 1. Introdução Breve: Por que Vue.js? (10 min)

O Vue.js é um **framework JavaScript progressivo** para a construção de interfaces de usuário. O termo "progressivo" significa que ele é projetado para ser **adotado incrementalmente**.

Você pode usá-lo para:

- **Melhorar um projeto existente** (adotando-o em uma pequena parte).
- **Construir uma SPA (Single Page Application)** do zero, como faremos neste projeto.

**Conceitos Chave:**

- **Componentes:** Unidades reutilizáveis e isoladas de interface (como nosso futuro `<TaskItem/>`).
- **Reatividade:** Atualização automática do DOM ao alterar o estado (_data_) de um componente.

---

### 🧰 2. Vue CLI: A Caixa de Ferramentas (5 min)

Para iniciar um projeto moderno com Vue, usamos a **Vue CLI (Command Line Interface)**.

**Vantagens:**

1. Configuração automática de ferramentas como Webpack e Babel.
2. Inclusão facilitada de plugins (Vuex, Vue Router).
3. Servidor local com _Hot Reload_.

---

### ⚙️ 3. Exercício: Configuração e Inicialização do Projeto (25 min)

#### ✅ Passo 1: Verificação de Pré-requisitos

Certifique-se de ter o Node.js (v12+) instalado.

Instale a Vue CLI globalmente:

```bash
npm install -g @vue/cli
```

Verifique a instalação:

```bash
vue --version
```

#### 🛠️ Passo 2: Criação do Projeto

Crie o projeto:

```bash
vue create gerenciador-tarefas
```

**Selecione:**

- `Manually select features`
- Marque:

  - `Babel`
  - `Router`
  - `Vuex`
  - `Linter / Formatter`

**Responda:**

- Use history mode for router? → **Yes**
- Pick a linter / formatter config → **ESLint + Prettier**
- Pick additional lint features → **Lint on save**
- Where do you prefer placing config? → **In dedicated config files**
- Save this as a preset? → **No**

#### 🧹 Passo 3: Limpeza Inicial

1. Entre no diretório:

```bash
cd gerenciador-tarefas
```

2. Abra no VS Code (ou outro editor):

```bash
code .
```

3. **Limpe o `src/views/Home.vue`:**

- Apague os conteúdos de `<template>`, `<script>` e `<style>`, deixando-os vazios.

4. **Limpe o `src/App.vue`:**

Substitua por:

```vue
<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
/* Opcional: remover qualquer estilo inicial */
</style>
```

_Próximo Capítulo: Componentização e Props._

---

### ✅ 5. Verificação Final (5 min)

1. Execute o projeto:

```bash
npm run serve
```

2. Acesse: [http://localhost:8080/](http://localhost:8080/)
   (Página em branco confirma que o setup está correto.)

3. Faça o commit inicial:

```bash
git init
git add .
git commit -m "Capítulo 1: Setup do Projeto e Estrutura Inicial"
```

---

🎉 **Fim da Aula 1.** Seu ambiente está configurado, as ferramentas principais selecionadas, e o projeto está pronto para a próxima fase: **Componentização**!
