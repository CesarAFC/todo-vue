<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])
const filteredTodos = computed(() => {
    return hideCompleted.value ? todos.value.filter( todo => !todo.done) : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((el) => el !== todo)
}
</script>

<template>
    <section class="todo-list">
        <form @submit.prevent="addTodo">
            <input class="input-form" v-model="newTodo" required placeholder="new todo">
            <button class="addTodo__button">Add Todo</button>
        </form>
        <ul>
            <p v-if="filteredTodos.length === 0">No pending todo</p>
            <li v-for="todo in filteredTodos" :key="todo.id">
                <input type="checkbox" v-model="todo.done">
                <span :class="{ done: todo.done }">{{ todo.text }}</span>
                <button class="delete__button" @click="removeTodo(todo)">x</button>
            </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
            {{ hideCompleted ? 'Show all' : 'Hide completed' }}
        </button>
    </section>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
.input-form {
    padding: 4px 8px;
}
.todo-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
}
.addTodo__button {
    margin-left: 4px;
    border: none;
    padding: 4px 8px;
    background-color: #BED7DC;
    border-radius: 4px;
    transition: 0.5s;
}
.addTodo__button:hover {
    cursor: pointer;
    background-color: #B3C8CF;
}
.delete__button {
    margin-left: 4px;
    width: 20px;
    height: auto;
    padding: 4px;
    border: none;
    background-color: #FA7070;
    transition: 0.2s;
    border-radius: 4px;
}
.delete__button:hover {
    cursor: pointer;
    background-color: #f94f4f;
}
</style>