<script setup>
import { ref } from 'vue';

const studentList = ref();

onMounted(async () => {
  const response = await fetch(
    'https://pb.seiwald.club/api/collections/4bhk/records'
  );
});
</script>

<template>
  <h1>Our Students:</h1>
</template>
