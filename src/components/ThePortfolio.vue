<script setup>
import { ref, defineProps } from 'vue';
import WelcomeItem from './WelcomeItem.vue';

// If your component has props you can define them like this:
const props = defineProps(['uid']);

// Method to handle the emitted event
const handleUidUpdate = (updatedUid) => {
  console.log("Received uid:", updatedUid);
};
</script>

<template>
  <WelcomeItem @update:uid="updateUID">
    <h1>hello folio</h1>
  </WelcomeItem>
</template>