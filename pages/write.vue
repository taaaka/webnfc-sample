<script setup lang="ts">
import { ref } from "vue";

const text = ref('');
const isWriteReady = ref(false);

const handleStandbyNFC = async () => {
  isWriteReady.value = true
  console.log(text.value)

  const reader = new NDEFReader();
  await reader.write(text.value);

  isWriteReady.value = false;
}

</script>

<template>
  <div>
    <h1>WebNFC Example (Writer)</h1>
    <hr>
    <input type="text" v-model="text">
    <button @click="handleStandbyNFC">Write NFC</button>
    <p v-if="isWriteReady">Write Stanby...</p>
  </div>
</template>