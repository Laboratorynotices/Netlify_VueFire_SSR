<script setup lang="ts">
const { data } = await useFetch("/api/hello");
const user = useCurrentUser();

console.log(user);
</script>

<template>
  <div>
    <pre>{{ data }}</pre>
    <pre>{{ user }}</pre>
  </div>
</template>
