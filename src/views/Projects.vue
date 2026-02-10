<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, onMounted } from 'vue'
import { projects } from '@/assets/Projects.js'

const projetos = ref([])
const projetosFiltrados = ref([])
const categoriaSelecionada = ref('todos')
const dropdownAberto = ref(false)
const categoriasUnicas = ref([])

const projetoSelecionado = ref(null)
const modalAberto = ref(false)
const imagemAtualIndex = ref(0)

const toggleDropdown = () => {
  dropdownAberto.value = !dropdownAberto.value
}

const fecharDropdown = () => {
  setTimeout(() => {
    dropdownAberto.value = false
  }, 200)
}

const filtrarCategoria = (categoria) => {
  categoriaSelecionada.value = categoria
  projetosFiltrados.value =
    categoria === 'todos'
      ? projetos.value
      : projetos.value.filter(p => p.category === categoria)

  dropdownAberto.value = false
}

const openModal = (projeto) => {
  projetoSelecionado.value = projeto
  imagemAtualIndex.value = 0
  modalAberto.value = true
}

const closeModal = () => {
  modalAberto.value = false
}

const prevImage = () => {
  const total = projetoSelecionado.value?.images.length || 1
  imagemAtualIndex.value = (imagemAtualIndex.value - 1 + total) % total
}

const nextImage = () => {
  const total = projetoSelecionado.value?.images.length || 1
  imagemAtualIndex.value = (imagemAtualIndex.value + 1) % total
}

onMounted(() => {
  projetos.value = projects
  projetosFiltrados.value = projects
  categoriasUnicas.value = [
    ...new Set(projects.map(p => p.category))
  ]
})
</script>

<template>
  <section class="projects-container">
    <h2>Meus Projetos</h2>
    <div class="filter-container">
      <div class="filter-dropdown" @click="toggleDropdown" tabindex="0" @blur="fecharDropdown">
        <div class="dropdown-header">
          {{ categoriaSelecionada === 'todos' ? 'Todos os projetos' : categoriaSelecionada }}
          <span class="arrow">&#9662;</span>
        </div>
        <ul v-if="dropdownAberto" class="dropdown-options">
          <li @click="filtrarCategoria('todos')">Todos os projetos</li>
          <li v-for="cat in categoriasUnicas" :key="cat" @click="filtrarCategoria(cat)">{{ cat }}</li>
        </ul>
      </div>
    </div>
    <div class="projects-grid">
      <div v-for="projeto in projetosFiltrados" :key="projeto.id" class="project-card">
        <img :src="projeto.images[0]" :alt="projeto.title">
        <h3>{{ projeto.title }}</h3>
        <p>{{ projeto.shortDescription }}</p>
        <button @click="openModal(projeto)" class="btn-see-more">Ver Mais</button>
      </div>
    </div>
    <div class="modal" :class="{ show: modalAberto }" @click="closeModal">
      <div class="modal-content" @click.stop>
        <span class="close" @click="closeModal">&times;</span>
        <h2>{{ projetoSelecionado?.title }}</h2>

        <div v-if="projetoSelecionado" class="carousel">
          <button class="prev" @click="prevImage">&#10094;</button>
          <img :src="projetoSelecionado.images[imagemAtualIndex]" :alt="projetoSelecionado.title">
          <button class="next" @click="nextImage">&#10095;</button>
        </div>
        <p>{{ projetoSelecionado?.detailedDescription }}</p>

        <div class="modal-buttons">
          <a v-if="projetoSelecionado?.githubUrl" :href="projetoSelecionado.githubUrl" target="_blank" class="btn"><i
              class="bi bi-github"></i> Código</a>
          <a v-if="projetoSelecionado?.siteUrl" :href="projetoSelecionado.siteUrl" target="_blank" class="btn"><i
              class="bi bi-globe"></i> Site</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.filter-dropdown {
  position: relative;
  width: 250px;
  user-select: none;
  cursor: pointer;
  margin-bottom: 20px;
}

.dropdown-header {
  padding: 12px 16px;
  border-radius: 8px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.arrow {
  transition: transform 0.3s ease;
}

.filter-dropdown:focus-within .arrow {
  transform: rotate(180deg);
}

.dropdown-options {
  list-style: none;
  padding: 0;
  margin: 5px 0 0;
  background-color: #000;
  border: 1px solid #379ab8;
  border-radius: 8px;
  position: absolute;
  width: 100%;
  z-index: 10;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);
}

.dropdown-options li {
  padding: 12px 16px;
  border-bottom: 1px solid #379ab8;
  transition: background-color 0.3s ease;
}

.dropdown-options li:last-child {
  border-bottom: none;
}

.dropdown-options li:hover {
  background-color: #379ab8;
  color: white;
}

.filter-container {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 20px;
}


.projects-container {
  padding: 2rem;
  color: white;
  margin-left: 200px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.profect-card {
  border-radius: 12px;
  padding: 1rem;
  text-align: center;
}

.project-card img {
  max-width: 100%;
  border-radius: 8px;
}

button.btn-see-more {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background: #379ab8;
  border: none;
  border-radius: 6px;
  color: white;
  cursor: pointer;
}

h3 {
  color: #379ab8;
}

p {
  font-size: 14px;
  color: #ccc;
}

.modal {
  display: none;
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);
  justify-content: center;
  align-items: center;
  overflow-y: auto;
}

.modal.show {
  display: flex;
}

.modal-content {
  background: #1a1a1a;
  padding: 2rem;
  border-radius: 12px;
  max-width: 800px;
  width: 90%;
  position: relative;
  color: white;
}

.close {
  position: absolute;
  top: 10px;
  right: 20px;
  font-size: 2rem;
  cursor: pointer;
}


.carousel {
  display: flex;
  align-items: center;
  margin: 1rem 0;
}

.carousel img {
  max-width: 90%;
  border-radius: 8px;
}

.carousel button {
  background: transparent;
  border: none;
  font-size: 2rem;
  color: #379ab8;
  cursor: pointer;
}

.modal-buttons {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.modal-buttons .btn {
  background: #379ab8;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  color: white;
  text-decoration: none;
}

@media (max-width: 1024px) {
  .projects-container {
    margin-left: 120px;
  }

  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .projects-container {
    margin-top: 8rem; /* espaço pro botão sanduíche */
    margin-left: 0;
    padding: 1rem;
  }

  .filter-container {
    justify-content: center;
  }

  .filter-dropdown {
    width: 100%;
  }

  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .modal-content {
    padding: 1rem;
  }

  .carousel img {
    max-width: 100%;
  }

  .modal-buttons {
    flex-direction: column;
  }

  .modal-buttons .btn {
    width: 100%;
    text-align: center;
  }
}
</style>
