<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <div style="height: 740px;" :style="{ backgroundColor: awesome ? 'black' : 'initial', color: awesome ? 'white' : 'initial' }">
  <button @click="toggle">切換模式</button>
  <h1 v-if="awesome">夜晚</h1>
  <h1 v-else>白天</h1>
  </div>
</template>