<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <button class="menu-sandwich" @click="sandwichMenu">
      <i :class="isOpen ? 'bi bi-x-lg' : 'bi bi-list'"></i>
    </button>

    <aside :class="['sidebar', { open: isOpen || isDesktop }]">
      <nav>
        <ul class="direction">
          <li><router-link to="/" @click="closeMenu">Sobre</router-link></li>
          <li><router-link to="/projects" @click="closeMenu">Projetos</router-link></li>
        </ul>
        <ul class="social">
          <li><a href="https://github.com/LeticiaAvelar" target="_blank"><i class="bi bi-github"></i></a></li>
          <li><a href="https://www.linkedin.com/in/leticia-avelar95/" target="_blank"><i class="bi bi-linkedin"></i></a>
          </li>
          <li><a href="mailto:leticia.avelar95@gmail.com" target="_blank"><i class="bi bi-envelope-fill"></i></a></li>
        </ul>
      </nav>
    </aside>
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount, onMounted } from 'vue'

const isOpen = ref(false)
const isDesktop = ref(window.innerWidth > 768)

const sandwichMenu = () => {
  isOpen.value = !isOpen.value
}

const closeMenu = () => {
  if (!isDesktop.value) isOpen.value = false
}

const handleResize = () => {
  isDesktop.value = window.innerWidth > 768
  if (isDesktop.value) isOpen.value = false
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
  handleResize()
})
onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100px;

  padding: 2rem 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  z-index: 1000;
  transform: translateX(0);
  transition: transform 0.3s ease;
}

.sidebar nav {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 1;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar li {
  margin-bottom: 1.5rem;
}

.sidebar a {
  color: #fff;
  text-decoration: none;
  font-weight: bold;
}

.sidebar .social a {
  font-size: 1.2rem;
  transition: 0.3s ease, color 0.3s ease;
}

.sidebar .social a:hover {
  transform: scale(1.5);
  color: #379ab8;
}

.sidebar .direction a:hover {
  color: #379ab8;
}

.menu-sandwich {
  background: none;
  border: none;
  color: #fff;
  font-size: 1.5rem;
  position: fixed;
  top: 1rem;
  left: 1rem;
  z-index: 2001;
  display: none;
}

@media (max-width: 768px) {
  .menu-sandwich {
    display: block;
  }

  .sidebar {
    width: 150px;
    transform: translateX(-100%);
  }

  .sidebar.open {
    transform: translateX(0);
  }
}
</style>
