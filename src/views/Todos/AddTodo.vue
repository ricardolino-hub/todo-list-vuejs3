<template>
    <div>
        <h1>Adicionar nova tarefa</h1>

        <form action="#" method="post" @submit.prevent="addTodo">
            <input type="text" name="name" placeholder="Titulo" v-model="todo.name">
            <input type="text" name="description" placeholder="Descrição" v-model="todo.description">
            <button type="submit" :disabled="todo.loadind">
                <span v-if="todo.loadind">Enviando</span>
                <span v-else>Enviar</span>
            </button>
        </form>
    </div>
</template>

<script>
import { reactive } from 'vue'
import TodoService from '@/services/todos.service'
import router from '@/router'

export default {
    name: 'AddTodo',
    setup() {
         const todo = reactive({
            name: '',
            description: '',
            completed: false,
            loadind: false
         })

        const addTodo = () => {
            todo.loadind = true
            TodoService.addTodo({...todo})
                        .then(() => router.push({name: 'todos.index'}))
                        .finally(() => todo.loadind = false)
        }

        return {
            addTodo,
            todo
        }
    }
}
</script>