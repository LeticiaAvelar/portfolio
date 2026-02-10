<!-- eslint-disable vue/multi-word-component-names -->
<script setup>

</script>

<template>
  <div class="about-container">
    <div class="about-text">
      <h1>Olá, eu sou a <span style="color: #379ab8;">Letícia Avelar</span> </h1>
      <p>Desenvolvedora Web | Quality Assurance (QA)</p>
      <p>Entre código, testes e aprendizado constante
        <br />
        <br />
        Atuo entre desenvolvimento e qualidade, com foco em lógica, testes e experiência do usuário.
        <br />
        Stack principal: HTML, CSS, JavaScript, Vue.js e Git.
        <br />
        Experiência com testes funcionais e de regressão, sempre buscando código claro, processos organizados e produtos
        confiáveis.
      </p>
      <div class="icons-grid">
        <i class="devicon-html5-plain colored"></i>
        <i class="devicon-css3-plain colored"></i>
        <i class="devicon-javascript-plain colored"></i>
        <i class="devicon-postgresql-plain colored"></i>
        <i class="devicon-dbeaver-plain"></i>
        <div class="break-line"></div>
        <i class="devicon-vuejs-plain colored"></i>
        <i class="devicon-bootstrap-plain colored"></i>
        <i class="devicon-python-plain colored"></i>
        <i class="devicon-laravel-original colored"></i>
        <i class="devicon-postman-plain colored"></i>
        <i class="devicon-cypressio-plain"></i>
      </div>
    </div>
    <div class="about-photo">
      <img src="/src/assets/my-photo.png" alt="minha foto">
    </div>
  </div>
</template>

<style scoped>
.about-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin: 8rem 2rem 2rem 2rem;
  margin-left: 200px;
}

.about-text {
  flex: 1;
  padding: 2rem;
}

.about-photo {
  display: flex;
  justify-content: center;
}

.about-photo img {
  width: 100%;
  max-width: 500px;
  height: auto;
}

.icons-grid {
  margin-top: 32px;
  background-color: #101720;
  border-radius: 20px;
  box-shadow: 0 0 10px #379ab8;
  padding: 2rem;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}

.break-line {
  flex-basis: 100%;
  height: 0;
}

.icons-grid i {
  font-size: 48px;
  transition: transform 0.3s ease;
}

.icons-grid i:hover {
  transform: scale(1.2);
}

@media (max-width: 768px) {
  .about-container {
    flex-direction: column;
    margin-left: 0;
    text-align: center;
  }

  .about-photo img {
    margin: 0 auto;
    width: 250px;
  }

  .about-text {
    padding: 1rem;
  }

  .icons-grid {
    padding: 1rem;
    gap: 1.5rem;
  }

  .icons-grid i {
    font-size: 36px;
  }
}
</style>
