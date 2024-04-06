<script setup lang='ts'>
defineProps({
  msg: String
})
</script>

<template>
  <h2>{{ msg || 'No props passed yet' }}</h2>
  <section></section>
</template>

<style scoped>

</style>