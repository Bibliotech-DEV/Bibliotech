<template>
  <div>
    <NavBar />
    <main class="main-section">
      <!--Inicio de contenido de la página index-->
      <div class="line-container">
        <h1>¡Bienvenido!</h1>
        <h3>a nuestro sistema bibliotecario</h3>
      </div>
      <b-container fluid-grow>
        <!--Sección para imagen y video central de los libros de Bibliotech-->
        <div class="banner-video">
          <div class="video-container">
            <video autoplay muted loop poster="../assets/images/banner.png">
              <source
                src="../assets/images/banner-video.mp4"
                type="video/mp4"
              />
            </video>
          </div>
        </div>
        <!--Saludo e invitación a ir a préstamo-->
        <div class="banner-text">
          <h3>¡Hola!</h3>
          <h5>¿Necesita un libro?</h5>
          <div class="button-solitude">
            <router-link to="Trade">Préstamo</router-link>
          </div>
        </div>
        <div class="space" />
      </b-container>
    </main>
    <Footer />
  </div>
</template>
<script>
import NavBar from "../components/navbar.vue";
import Footer from "../components/footer.vue";

export default {
  components: {
    NavBar,
    Footer,
  },
};
</script>
