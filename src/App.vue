<script setup lang="ts">
import { useStreamerbot } from '@streamerbot/vue';
import { onMounted, ref } from 'vue';

const { client, status, connect } = useStreamerbot();

const messages = ref<any[]>([]);

onMounted(async () => {
  await connect();

  client.value?.on('Twitch.ChatMessage', ({ data }: any) => {
    messages.value.push(data.message);
  });
});


</script>

<template>
  <h2>Streamer.bot</h2>
  <div>Connection Status: {{ status }}</div>
  <div v-for="message in messages" :key="message.msgId">
    {{ message.displayName }}: {{ message.message }}
  </div>
</template>

<style scoped></style>
