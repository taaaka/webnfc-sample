<script setup lang="ts">
import { ref } from "vue";

const reading = ref(false);

const handleStandbyNFC = async () => {
  const reader = new NDEFReader();
  await reader.scan();

  reader.addEventListener('reading', (e) => {
    console.log(e);
    reading.value = true;
  })

  reader.addEventListener('readingerror', (e) => {
    console.error(e);
  })
}

</script>

<template>
  <div>
    <h1>WebNFC Example</h1>
    <hr>
    <p v-if="reading">Read finish</p>
    <button @click="handleStandbyNFC">Read NFC</button>
  </div>
</template>