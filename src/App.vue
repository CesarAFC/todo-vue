<script setup lang="ts">
import Todo from './components/Todo.vue'
import ApiCall from './components/ApiCall.vue'
import PresentationCard from './components/PresentationCard.vue'
</script>
<template>
  <section class="app">
    <Todo />
    <ApiCall />
  </section>
  <PresentationCard msg="Hello from App or Parent" />
</template>

<style scoped>
  .app {
    margin: 20px;
    display: flex;
    justify-content: flex-start;
    gap: 20px
  }
</style>
