<script setup lang="ts">
import { ref } from "vue";

const count = ref(0)
const reading = ref(false);

const handleClick = () => {
  count.value++;
}

const handleStandbyNFC = async () => {
  const reader = new NDEFReader();
  await reader.scan();

  reader.addEventListener('reading', (e) => {
    console.log(e);
    reading.value = true;
  })
}

</script>

<template>
  <div>
    <h1>Hello, Nuxt 3!</h1>
    <button @click="handleClick">Count up {{count}}</button>
    <hr>
    <p v-if="reading">Read finish</p>
    <button @click="handleStandbyNFC">Read NFC</button>
  </div>
</template>