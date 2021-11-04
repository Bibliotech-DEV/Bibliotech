<template>
  <div class="d-flex">
    <!-- Barra de navegación -->
    <aside class="d-flex flex-column barra-lateral">
      <SideBar :option="2" />
    </aside>
    <!-- FIN Barra de navegación -->

    <!-- Contenido principal de la pagina -->
    <main class="contenido">
      <!-- Parte superior (Migas de pan y botones) -->
      <div class="barra-superior">
        <div class="contenedor-superior">
          <!-- Migas de pan -->
          <div class="contenedor-migasdepan">
            <MigaMain title="Artículos" />
          </div>
          <!-- FIN Migas de pan -->

          <!-- Botones con funciones -->
          <BotonNuevo />
        </div>
      </div>
      <!-- FIN Parte superior (Migas de pan y botones) -->

      <!-- Contenido luego de las migas de pan (Cartas) -->
      <div class="seccion-central">
        <!-- Grilla dinamica -->
        <div class="grilla-responsive">
          <Tarjeta
            v-for="(articulo, index) in articulos"
            :key="index"
            :index="index"
            :articulo="articulo"
          />
        </div>
        <!-- FIN Grilla dinamica -->
      </div>
      <!-- FIN Contenido luego de las migas de pan (Cartas) -->
    </main>
    <!-- FIN Contenido principal de la pagina -->
  </div>
</template>
<script>
import SideBar from "../components/SideBar.vue";
import Tarjeta from "../components/contentManagers/CardEditItem.vue";
import MigaMain from "../components/BreadCrumbsMain.vue";
import BotonNuevo from "../components/contentManagers/NewBook.vue";

export default {
  components: {
    SideBar,
    Tarjeta,
    MigaMain,
    BotonNuevo,
  },
  data() {
    return {
      /*items: [
        { book_title: 'Science & Technology', book_author: 'Ravi Agrahari', image:'placeholder.png'},
        { book_title: 'Introducing Go', book_author: 'Caleb Doxsey', image:'placeholder.png'},
        { book_title: 'Programa o serás programado', book_author: 'Douglas Rushkoff', image:'placeholder.png'},
        { book_title: 'New Yorker Issue Vol 85-26', book_author: 'The New Yorker', image:'placeholder.png'}
      ]*/
      url: "https://bibliotech-conection.herokuapp.com/api/articulos",
      articulos: [
        {
          id: "",
          nombre: "",
          prestamo: "",
          nombre_editorial: "",
          nombre_autor: "",
          nombre_categoria: "",
          isbn: "",
        },
      ],
    };
  },
  created() {
    this.mostrar();
  },
  methods: {
    mostrar() {
      this.axios.get(this.url).then((response) => {
        this.articulos = response.data;
      });
    },
  },
};
</script>
<style scoped>
.barra-lateral {
  background-color: white;
  width: 16vw;
  height: 100vh;
  border-right: 1px solid #0000001f;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.082), 0 1px 2px rgba(0, 0, 0, 0.158);
}
.contenido {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: space-around;
  width: 84vw;
}
.barra-superior {
  display: flex;
  justify-content: center;
  height: 6.25rem !important;
  width: 100%;
  padding-top: 40px !important;
  padding-bottom: 40px !important;
  margin-top: 20px;
}
.contenedor-superior {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 100%;
  height: 100%;
  padding-left: 3.75rem;
}
.contenedor-migasdepan {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 100%;
}
.contenedor-botonessuperiores {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 100%;
}
.boton__crear {
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #ff6c38;
  width: 2.375rem;
  height: 2.375rem;
  border-radius: 4px;
  box-sizing: border-box;
  margin-right: 1.25rem;
  cursor: pointer;
}
.boton__crear:hover {
  background-color: #db5f32;
}
.icono-superior {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;
}
.material-icons--boton-sup {
  color: #ffffff;
  font-size: 2.375rem;
}
.material-icons--boton-sup-fixed {
  color: #ffffff;
  font-size: 1.7rem;
}
.boton__seleccionar {
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #485eb2;
  width: 2.375rem;
  height: 2.375rem;
  border-radius: 4px;
  box-sizing: border-box;
  margin-right: 1.25rem;
}
.boton__borrar {
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #c30000;
  width: 2.375rem;
  height: 2.375rem;
  border-radius: 4px;
  box-sizing: border-box;
  margin-right: 1.25rem;
}
.boton__editar {
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #485eb2;
  width: 2.375rem;
  height: 2.375rem;
  border-radius: 4px;
  box-sizing: border-box;
  margin-right: 1.25rem;
  padding: 6px;
  cursor: pointer;
}
.boton__editar:hover {
  background-color: #3a4b8d;
} /* FIN Botones superiores */
/* Migas de pan */
.migas__principal--texto {
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  font-size: 2.125rem;
  letter-spacing: 0.016rem;
}
.migas__principal--texto a {
  text-decoration: none;
  color: #aaaaaa;
}
.miga1 {
  color: #aaaaaa;
}
.separador {
  color: #aaaaaa;
  padding-left: 2rem;
  padding-right: 2rem;
}
/* FIN migas de pan */
.seccion-central {
  width: 100%;
  height: 100%;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  box-sizing: border-box;
}
.grilla-responsive {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 0.46fr));
  grid-template-rows: repeat(1, 300px);
  grid-gap: 1rem;
  grid-auto-flow: dense;
  justify-items: center;
  box-sizing: border-box;
  padding-bottom: 40px;
}
@media (min-width: 1234px) {
  .grilla-responsive {
    grid-template-columns: repeat(auto-fit, minmax(260px, 0.46fr));
  }
  .barra-lateral {
    height: 100%;
  }
}
@media (max-width: 1233px) {
  .barra-lateral {
    height: 100%;
  }
}
@media (min-width: 1367px) {
  .grilla-responsive {
    grid-template-columns: repeat(auto-fit, minmax(320px, 0.46fr));
  }
  .barra-lateral {
    height: 100%;
  }
}
@media (min-width: 1658px) {
  .barra-lateral {
    height: 51vw;
  }
}
</style>
