<template>
  <h1>
    Lista de tarefas
    <router-link :to ="{name: 'todos.create'}">+</router-link>
  </h1>

  <div v-show="loading">Carregando as tarefas</div>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
    </li>
  </ul>
</template>

<script>
import { onMounted, ref } from 'vue'
import TodoService from '@/services/todos.service'

export default {
  setup() {
    const todos = ref([])

    const loading = ref(false)

    onMounted(() => {
      loading.value = true
      TodoService.getAll()
               .then(response => todos.value = response.data.data)
               .catch(error => console.log(error))
               .finally(() => loading.value = false)
    })

    return {
      loading,
      todos
    }
  }
}
</script>

<style scope>

</style>