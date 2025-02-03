<script setup lang="ts">
const { data } = await useFetch("/api/hello");
</script>

<template>
  <div>
    <pre>{{ data }}</pre>
  </div>
</template>
