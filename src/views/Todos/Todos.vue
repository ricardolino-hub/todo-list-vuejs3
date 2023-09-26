<template>
  <h1>Lista de tarefas</h1>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.name }}
    </li>
  </ul>
</template>

<script>
export default {
  setup() {
    const todos = [
      {
        id: 1,
        name: 'Tarefa 01',
        completed: true
      },
      {
        id: 2,
        name: 'Tarefa 02',
        completed: true
      },
      {
        id: 3,
        name: 'Tarefa 03',
        completed: true
      }
    ]

    return {
      todos
    }
  }
}
</script>

<style scope>

</style>