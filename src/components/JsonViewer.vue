<script setup lang="ts">
import { ref } from 'vue'
import JsonViewer from 'vue-json-viewer'

defineProps<{
  value: Object
}>()

</script>

<template>
  <json-viewer :value="value" :expand-depth=100 copyable boxed expanded></json-viewer>
</template>
