<template>
    <div>{{ result }}</div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['valA', 'valB']);
  const result = ref(0);
  
  watch([() => props.valA, () => props.valB], ([newValA, newValB]) => {
    result.value = newValA * (newValB / 100);
  });
  </script>
  