<template>
  <section class="todo-list">
    <h3>Lista de Tarefas</h3>

    <div class="all-todos">
      <div
        v-for="todo in todos"
        :key="todo"
        class="single-todo"
        :class="{ done: todo.done }"
      >
        <p>{{ todo.text }}</p>
      </div>
    </div>

    <button class="clear">Limpar tudo</button>

    <input
      type="text"
      placeholder="Escreva uma nova tarefa..."
      v-model="newTodo.text"
    />
    <button class="add" @click="addTodo()">Adicionar</button>
    <p class="error" :class="{ errorDisplay: error }">Por favor, digite algo</p>

    <div class="instructions">
      Instruções:
      <ul>
        <li>Clique no texto da tarefa para alternar entre feita / não feita</li>
        <li>Use o botão limpar tudo para remover todas as tarefas</li>
        <li>Use o input para adicionar novas tarefas</li>
      </ul>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: {
        text: "",
        done: false,
      },
      error: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.text) {
        this.todos.push(this.newTodo);
        this.newTodo = {
          text: "",
          done: false,
        };
        this.error = false;
      } else {
        this.error = true;
      }
    },
  },
};
</script>
<style>
.todo-list input {
  box-sizing: border-box;
  height: 28px;
  border-radius: 0.25rem;
  width: 60%;
  border: 1px solid lightgrey;
  margin-top: 32px;
}

button {
  background-color: transparent;
  cursor: pointer;
  box-sizing: border-box;
  height: 28px;
  border-radius: 0.25rem;
  color: #fff;
}

button:hover {
  opacity: 0.8;
}

button.add {
  background-color: #007bff;
  border: 1px solid #007bff;
  margin-left: 2px;
}

button.clear {
  background-color: #dc3545;
  border: 1px solid #dc3545;
  display: block;
  margin: auto;
}

button:focus {
  outline: 0;
}

section.todo-list h3 {
  text-align: center;
  margin-top: 24px;
  width: 100%;
}

section.todo-list {
  flex-wrap: wrap;
  border: 1px solid lightgrey;
  background-color: rgb(248, 248, 248);
  padding: 20px;
  max-width: 500px;
  min-width: 300px;
  text-align: center;
  border-radius: 0.25rem;
}

.all-todos .single-todo {
  display: flex;
  align-items: center;
  justify-content: center;
}

.all-todos .single-todo p {
  margin: 12px 0;
  cursor: pointer;
}

.all-todos .single-todo.done p {
  text-decoration: line-through;
}

.all-todos .single-todo button.remove {
  width: 12px;
  height: 12px;
  border: none;
  background: transparent url("img/remove.png") no-repeat center;
  background-size: contain;
  cursor: pointer;
  margin-left: 8px;
}

section.todo-list button.clear {
  margin-top: 24px;
}

.error {
  font-size: 12px;
  margin-top: 10px;
  color: #dc3545;
  display: none;
}

.errorDisplay {
  display: block;
}

div.instructions {
  font-size: 11px;
  margin-top: 40px;
  color: grey;
}

div.instructions ul {
  list-style: inside;
  text-align: center;
  padding: 0;
}

div.instructions ul li {
  margin: 4px auto;
}
</style>
