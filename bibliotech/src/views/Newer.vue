<template>
  <div class="d-flex">
    <!-- Barra de navegación -->
    <aside class="d-flex flex-column barra-lateral">
      <SideBar :option="1" />
    </aside>
    <!-- FIN Barra de navegación -->
    <main class="contenido">
      <div class="seccion-central">
        <div class="segmentos-centrales">
          <!-- Contenedor rectangular que contiene a el titulo y a las tarjetas -->
          <div class="segmentos-centrales__contenedor">
            <!-- Titulo -->
            <div class="caja__titulo">
              <p class="mb-0 caja__titulo--estilos">Articulos Recientes</p>
            </div>
            <!-- FIN Titulo -->

            <!-- Envoltura para las cajas -->
            <div class="grilla-responsive">
              <Tarjeta
                v-for="(articulo, index) in articulos"
                :key="index"
                :index="index"
                :articulo="articulo"
              />
            </div>
            <!-- FIN Envoltura para las cajas -->
          </div>

          <!-- Separador central -->
          <div class="segmentos-centrales__separador">
            <div class="separador__caja"></div>
          </div>
          <!-- FIN Separador central -->

          <!-- Contenedor rectangular que contiene a el titulo y a las tarjetas -->
          <div class="segmentos-centrales__contenedor">
            <!-- Titulo -->
            <div class="caja__titulo">
              <p class="mb-0 caja__titulo--estilos">
                Administradores Recientes
              </p>
            </div>
            <!-- FIN Titulo -->

            <div class="grilla-responsive">
              <TarjetaAdmin
                v-for="(admin, index) in admins"
                :key="index"
                :index="index"
                :admin="admin"
              />
            </div>

            <!-- Envoltura para las cajas -->
            <!-- <div class="caja__cartas"> 
              <TarjetaAdmin
                v-for="(admin, index) in admins"
                :key="index"
                :index="index"
                :admin="admin"
              /> -->
            <!-- </div> FIN Envoltura para las cajas -->
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
<script>
import SideBar from "../components/SideBar.vue";
import Tarjeta from "../components/contentManagers/CardEditItem.vue";
import TarjetaAdmin from "../components/contentManagers/CardEditAdmin.vue";

export default {
  components: {
    SideBar,
    Tarjeta,
    TarjetaAdmin,
  },
  data() {
    return {
      url: "https://bibliotech-conection.herokuapp.com/api/articulos_recientes",
      url1: "https://bibliotech-conection.herokuapp.com/api/usuarios_recientes",
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
      admins: [
        {
          id: "",
          nombre: "",
          apellido: "",
          contraseña: "",
          usuario: "",
          correo: "",
        },
      ],
    };
  },
  created() {
    this.mostrarArticulos();
    this.mostrarAdmins();
  },
  methods: {
    mostrarArticulos() {
      this.axios.get(this.url).then((response) => {
        this.articulos = response.data;
      });
    },
    mostrarAdmins() {
      this.axios.get(this.url1).then((response) => {
        this.admins = response.data;
      });
    },
  },
};
</script>
<style scoped>
.barra-lateral {
  background-color: white;
  width: 16vw;
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
.seccion-central {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100vh;
  margin-top: 3rem;
  padding-right: 1.5rem;
  padding-left: 1.5rem;
  box-sizing: border-box;
}
.segmentos-centrales {
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}
.segmentos-centrales__contenedor {
  padding-left: 1px;
  display: flex;
  flex-direction: column;
  padding-bottom: 2px;
}
.caja__titulo {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 60px;
}
.caja__titulo--estilos {
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  font-size: 1.5rem;
  letter-spacing: 0.016rem;
}
.caja__cartas {
  background-color: blue;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: flex-start;
}

.caja__cartas2 {
  background-color: rgb(57, 20, 220);
}
.segmentos-centrales__separador {
  background-color: #0000001f;
  margin-top: 39px;
  margin-bottom: 20px;
}
.separador__caja {
  height: 1px;
  width: 100%;
}
@media (min-width: 768px) {
  .contenido {
    background-color: rgb(255, 255, 255);
  }
}
@media (min-width: 1233px) {
  .contenido {
    background-color: rgb(255, 255, 255);
  }
}
@media (min-width: 1366px) {
  .contenido {
    background-color: rgb(255, 255, 255);
  }
}
.caja__cartas1 {
  background-color: crimson;

  margin-right: 10px;
}
.cuadricula-tarjeta {
  padding: 10px;
  display: flex;
  justify-content: center;
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
