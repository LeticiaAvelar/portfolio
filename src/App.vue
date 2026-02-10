<script setup>
import Sidebar from './components/Sidebar.vue'

</script>

<template>
  <div class="app-container">
    <Sidebar /> <!-- é global, por isso fica fora -->
    <main class="main-content">
      <router-view />
    </main>
  </div>
</template>

<style>

</style>
