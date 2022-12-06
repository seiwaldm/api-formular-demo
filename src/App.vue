<script setup>
// Import your components here:
import HelloJOHAK from './components/HelloJOHAK.vue';
import StudentList from './components/StudentList.vue';
import StudentListPocketbase from './components/StudentListPocketbase.vue';
import RealtimeChatVue from '@/components/RealtimeChat/RealtimeChat.vue';
</script>

<template>
  <!-- Use your components here: -->
  <!-- <HelloJOHAK></HelloJOHAK> -->
  <!-- <StudentListPocketbase /> -->
  <RealtimeChatVue> </RealtimeChatVue>
  <div>
    <p>
      built with <img src="/vite.svg" alt="vite-logo" /> &
      <img src="/vue.svg" alt="" />
    </p>
  </div>
</template>
