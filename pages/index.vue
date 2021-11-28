<script setup lang="ts">
import { ref } from "vue";

const reading = ref(false);
const fortune = ref('');

const handleStandbyNFC = async () => {
  fortune.value = '';
  reading.value = true;

  const reader = new NDEFReader();
  await reader.scan();

  reader.addEventListener('reading', (e: NDEFReadingEvent) => {
    console.log(e);
    reading.value = false;

    const {serialNumber, message} = e;

    console.log(`> Serial Number: ${serialNumber}`);
      console.log(message);
      const record = message.records[0];
      const { data, encoding, recordType } = record;
      if (recordType === "text") {
        const textDecoder = new TextDecoder(encoding);
        fortune.value = textDecoder.decode(data);
      }
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
    <p v-if="fortune.length > 0">あなたの運勢は… {{fortune}}</p>
    <p v-if="reading">読み込み待機中…</p>
    <button @click="handleStandbyNFC">Read NFC</button>
  </div>
</template>