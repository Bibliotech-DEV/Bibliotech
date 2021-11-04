<template>
  <main class="main-section">
    <!--Inicio sección de saludo-->
    <div class="lineTrade-container">
      <h1>Solicitud</h1>
      <h3>de libro en préstamo</h3>
    </div>
    <b-container fluid>
      <div class="box-search">
        <div class="search-text">
          <label for="search-book">Búsqueda de artículos</label>
        </div>
        <div class="box">
          <b-form-input
            list="search-list"
            v-model="libro"
            id="search-book"
          ></b-form-input>
          <b-form-datalist id="search-list" :options="books"></b-form-datalist>
        </div>
        <div class="button">
          <b-button @click="mostrarCategoria(libro)">Buscar</b-button>
        </div>
      </div>
      <div>
        <div class="title-format">
          <h3>Categoría: {{ libro }}</h3>
          <!--Esta categoría se pinta con la lista y cambiar el nombre de categoría en la que se está-->
        </div>
        <b-row class="row-books">
          <b-col
            cols="12"
            md="6"
            lg="4"
            v-for="articulo in articulos"
            :key="articulo.id"
          >
            <!--Libro 1-->
            <div
              class="option-book"
              v-b-modal.modal-book6
              @click="llenarModal(articulo)"
            >
              <!--Imagen de categoría-->
              <span v-if="articulo.nombre_categoria == 'Académico'">
                <img
                  class="img-option"
                  src="../assets/images/academic.png"
                  fluid
                  alt="Un libro"
                />
              </span>
              <span v-else-if="articulo.nombre_categoria == 'Digital'">
                <img
                  class="img-option"
                  src="../assets/images/digital.png"
                  fluid
                  alt="Un libro"
                />
              </span>
              <span v-else-if="articulo.nombre_categoria == 'Ilustración'">
                <img
                  class="img-option"
                  src="../assets/images/illustration.png"
                  fluid
                  alt="Un libro"
                />
              </span>
              <span v-else-if="articulo.nombre_categoria == 'Manual'">
                <img
                  class="img-option"
                  src="../assets/images/manual.png"
                  fluid
                  alt="Un libro"
                />
              </span>
              <span v-else-if="articulo.nombre_categoria == 'Revista'">
                <img
                  class="img-option"
                  src="../assets/images/magazine.png"
                  fluid
                  alt="Un libro"
                />
              </span>
              <figcaption class="data-book">
                <!--Datos del libro-->
                <h4>Título: {{ articulo.nombre }}</h4>
                <!--Título-->
                <h5>Autor: {{ articulo.nombre_autor }}</h5>
                <!--Autor-->
              </figcaption>
            </div>
            <!--Modal con más información del libro y solicitud-->
          </b-col>
          <b-modal
            id="modal-book6"
            size="sm"
            centered
            ok-only
            hide-footer
            no-stacking
          >
            <p class="info-book">
              <!--Datos extra-->
              Formato: {{ dataModal.nombre_categoria }} <br />{{
                dataModal.nombre
              }}
              <br />{{ dataModal.nombre_autor }} <br />2004 <br />{{
                dataModal.nombre_editorial
              }}
              <br />ISBN {{ dataModal.isbn }} <br /><b>Disponible</b>
            </p>
            <div class="btn-solitude">
              <b-button v-b-modal.modal-solitude6>Solicitar</b-button
              ><!--Botón solicitar-->
            </div>
          </b-modal>
          <!--Modal con confirmación, se puede reemplazar por el plugin de sweet alert-->
          <b-modal id="modal-solitude6" size="sm" centered ok-only hide-footer>
            <div class="confirmed-box">
              <div class="box-check">
                <div class="confirmed-icon">
                  <b-icon icon="check-circle"></b-icon>
                </div>
                <p class="confirmed-text">¡Su préstamo ha sido exitoso!</p>
              </div>
            </div>
          </b-modal>
        </b-row>
      </div>
    </b-container>
    <!-- fin libros o articulos que se van a listar-->
  </main>
</template>
<script>
export default {
  data() {
    return {
      url: "https://bibliotech-conection.herokuapp.com/api/articulos/",
      url1: "https://bibliotech-conection.herokuapp.com/categorias/",
      articulos: [],
      books: ["Académico", "Digital", "Ilustración", "Manual", "Revista"],
      libro: "",
      dataModal: {
        id: null,
        nombre: "",
        prestamo: "",
        nombre_editorial: "",
        nombre_autor: "",
        nombre_categoria: "",
        isbn: "",
      },
      articulo: {
        id: null,
        nombre: "",
        prestamo: "",
        nombre_editorial: "",
        nombre_autor: "",
        nombre_categoria: "",
        isbn: "",
      },
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
    mostrarCategoria(categoria) {
      if (categoria == "") {
        this.mostrar();
      } else {
        this.axios.get(this.url1 + categoria).then((response) => {
          this.articulos = response.data;
        });
      }
    },
    llenarModal(art) {
      console.log(art);
      this.dataModal = art;
    },
  },
};
</script>
<style scoped>
.form-control {
  border: 1px solid #ff3000 !important;
}
.btn-secondary {
  background-color: #485eb2 !important;
  border: 1px solid #485eb2 !important;
}
/*Modal 1 solo cambia .modal-view*/
.modal-view {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
}
/*Organización de los libros*/
.option-book {
  margin-top: 2rem;
}
.option-book:hover {
  background-color: #d6d6d669;
}
.img-option {
  width: 55%;
}
</style>
