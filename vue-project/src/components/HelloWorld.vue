<template>
  <div id="app">
    <h1>Lista de Tarefas</h1>
    <div>
      <input v-model="newTask" placeholder="Digite uma nova tarefa">
      <button @click="addTask">Criar Tarefa</button>
      <ul>
        <li v-for="task in tasks" :key="task.id">
          {{ task.title }}
          <button @click="deleteTask(task.id)">Deletar</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: []
    };
  },
  methods: {
    fetchTasks() {
      fetch("https://jsonplaceholder.typicode.com/todos")
        .then(response => response.json())
        .then(data => {
          this.tasks = data;
        });
    },
    addTask() {
      if (this.newTask.trim() === "") return;
      
      const newTask = {
        userId: 1,
        title: this.newTask,
        completed: false
      };
      
      fetch("https://jsonplaceholder.typicode.com/todos", {
        method: "POST",
        body: JSON.stringify(newTask),
        headers: {
          "Content-Type": "application/json"
        }
      }).then(response => response.json())
        .then(data => {
          this.tasks.push(data);
          this.newTask = "";
          console.log(data); // Coloque o console.log dentro deste bloco
        });
    },
    deleteTask(taskId) {
      fetch(`https://jsonplaceholder.typicode.com/todos/${taskId}`, {
        method: "DELETE"
      }).then(() => {
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      });
    }
  },
  mounted() {
    this.fetchTasks();
  }
};
</script>
