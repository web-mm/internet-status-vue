<template>
  <div>
    <div :class="statusClass" class="status-dot"></div>
    <p>{{ message }}</p>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isOnline = ref(navigator.onLine);
const statusClass = ref('');
const message = ref('');

const updateStatus = () => {
  isOnline.value = navigator.onLine;
  statusClass.value = isOnline.value ? 'green-dot' : 'red-dot';
  message.value = isOnline.value ? 'You are online' : 'You are offline';
};

onMounted(() => {
  updateStatus();
  window.addEventListener('online', updateStatus);
  window.addEventListener('offline', updateStatus);
});

onUnmounted(() => {
  window.removeEventListener('online', updateStatus);
  window.removeEventListener('offline', updateStatus);
});
</script>

<style scoped>
.status-dot {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: inline-block;
  margin-right: 10px;
}

.green-dot {
  background-color: green;
}

.red-dot {
  background-color: red;
}
</style>
