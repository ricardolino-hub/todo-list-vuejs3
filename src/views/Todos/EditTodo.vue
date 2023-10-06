<template>
    <div>
        <h1>Editar tarefa</h1>

        <form action="#" method="post" @submit.prevent="editTodo">
            <input type="text" name="name" placeholder="Titulo" v-model="todo.name">
            <input type="text" name="description" placeholder="Descrição" v-model="todo.description">
            <button type="submit" :disabled="todo.loadind">
                <span v-if="todo.loadind">Carregando...</span>
                <span v-else>Enviar</span>
            </button>
        </form>
    </div>
</template>

<script>
import { onMounted, reactive } from 'vue'
import TodoService from '@/services/todos.service'
import router from '@/router'

export default {
    name: 'EditTodo',
    props: {
        id: {
            require: true
        }
    },
    setup(props) {
         const todo = reactive({
            name: '',
            description: '',
            completed: false,
            loadind: false
         })

         onMounted(async () => {
            todo.loadind = true
            TodoService.getTodo(props.id)
                        .then(response => {
                            const todoR = response.data.data
                            todo.name = todoR.title
                            todo.description = todoR.body
                            todo.completed = todoR.completed == 'S'
                        })
                        .finally(() => todo.loadind = false)
         })

        const editTodo = () => {
            todo.loadind = true
            TodoService.editTodo(props.id, {...todo})
                        .then(() => router.push({name: 'todos.index'}))
                        .finally(() => todo.loadind = false)
        }

        return {
            editTodo,
            todo
        }
    }
}
</script>