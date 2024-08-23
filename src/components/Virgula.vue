<template>
    <div>{{ result }}</div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['val']);
  const result = ref('');
  
  watch(() => props.val, (newVal) => {
    result.value = newVal.replace('.', ',');
  });
  </script>
  