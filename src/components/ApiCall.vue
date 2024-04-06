<script setup lang="ts">
import { ref, watch } from 'vue'

const todoId = ref(1)
const todoData = ref(null)
const loading = ref(false)

async function fetchData() {
  loading.value = true
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
  loading.value = false
}

fetchData()

watch(todoId, fetchData)

</script>

<template>
    <section class="api-call">
        <p>Todo id: {{ todoId }}</p>
        <button @click="todoId++" :disabled="!todoData">Fetch next todo</button>
        <p v-if="loading">Loading...</p>
        <pre v-else>{{ todoData }}</pre>
    </section>
</template>
<style scoped>
.api-call {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
}
</style>