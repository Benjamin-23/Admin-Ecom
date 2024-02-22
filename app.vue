<script setup lang="ts">
const usersData = await useFetch('http://localhost:3000/user')

</script>
<template>
  <div class="">
    <!-- <NuxtLayout name="default" /> -->
    <NuxtPage />
  </div>
</template>
<style></style>
