<script setup>
import ThePortfolio from '../components/ThePortfolio.vue'
</script>

<template>
  <div class="portfolio">
    <h1>PORTFOLIO PAGE</h1>
    <ThePortfolio />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
