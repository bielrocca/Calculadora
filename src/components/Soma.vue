
<template>
    <div>{{ resultado }}</div>
  </template>
  
  <script setup>
  import { defineProps, computed } from 'vue';
  
  const props = defineProps(['a', 'b']);
  
  const resultado = computed(() => {
    return props.a + props.b;
  });
  </script>