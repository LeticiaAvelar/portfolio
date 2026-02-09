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
html,
body,
#app {
  height: 100%;
  margin: 0;
  background-color: #212529; /* Gray 900 */
}
</style>
