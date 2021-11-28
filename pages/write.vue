<script setup lang="ts">
import { ref } from "vue";

const text = ref('');
const isReadReady = ref(false);

const handleStandbyNFC = async () => {
  isReadReady.value = true
  console.log(text.value)

  const reader = new NDEFReader();
  await reader.write(text.value);

  isReadReady.value = false;
}

</script>

<template>
  <div>
    <h1>WebNFC Example (Writer)</h1>
    <hr>
    <input type="text" v-model="text">
    <button @click="handleStandbyNFC">Read NFC</button>
    <p v-if="isReadReady">Read Stanby...</p>
  </div>
</template>