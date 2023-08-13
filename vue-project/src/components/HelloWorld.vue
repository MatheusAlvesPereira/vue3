<template>
  <h1>Lista de Tarefas</h1>
  <div>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Digite uma nova tarefa"/>
    <button @click="addTask">Add Task</button>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.title }}
        <button @click="deleteTask(task.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'TaskList',
  setup() {
    const newTask = ref('');
    const tasks = ref([]);

    const addTask = () => {
      if (newTask.value.trim() === '') return;

      const taskToAdd = {
        userId: 1,
        title: newTask.value,
        completed: false
      };

      fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST',
        body: JSON.stringify(taskToAdd),
        headers: {
          'Content-Type': 'application/json'
        }
      })
        .then(response => response.json())
        .then(data => {
          tasks.value.push(data);
          newTask.value = '';
        });
    };

    const deleteTask = taskId => {
      fetch(`https://jsonplaceholder.typicode.com/todos/${taskId}`, {
        method: 'DELETE'
      })
        .then(() => {
          tasks.value = tasks.value.filter(task => task.id !== taskId);
        });
    };

    return {
      newTask,
      tasks,
      addTask,
      deleteTask
    };
  }
};
</script>
