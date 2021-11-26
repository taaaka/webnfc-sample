<script setup lang="ts">
import { ref } from "vue";

const count = ref(0)

const handleClick = () => {
  count.value++;
}
</script>

<template>
  <div>
    <h1>Hello, Nuxt 3!</h1>
    <button @click="handleClick">Count up {{count}}</button>
  </div>
</template>