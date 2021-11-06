<template>
  <div class="contenedor-botonessuperiores">
    <!-- Boton para crear elementos -->
    <div v-b-modal.modal-creation class="boton__crear">
      <!-- <div v-b-modal="`modal-${index}` " @click="editItem()" class="boton__crear"> -->
      <div class="icono-superior">
        <span class="mb-0 material-icons material-icons--boton-sup">add</span>
      </div>
    </div>
    <!-- FIN Boton para crear elementos -->

    <b-modal id="modal-creation" title="Nuevo Artículo" hide-footer centered>
      <!-- <b-modal class="titulo-modal" :id="`modal-${index}`" title="Nuevo Artículo" hide-footer> -->

      <b-form @submit="onSubmit">
        <b-container>
          <b-row>
            <b-col>
              <div class="form-floating mt-4 mb-4">
                <input
                  v-model="form.isbn"
                  type="text"
                  class="mb-0 form-control"
                  id="floatingInput"
                  placeholder=""
                />
                <label label for="mb-0 floatingInput" class="text-secondary"
                  >ISBN</label
                >
              </div>
            </b-col>
          </b-row>

          <b-row>
            <b-col>
              <div class="form-floating mb-4">
                <input
                  v-model="form.nombre"
                  type="text"
                  class="mb-0 form-control"
                  id="floatingInput"
                  placeholder=""
                />
                <label label for="mb-0 floatingInput" class="text-secondary"
                  >Nombre del artículo</label
                >
              </div>
            </b-col>
          </b-row>

          <b-row>
            <b-col>
              <div class="form-floating mb-4">
                <input
                  v-model="form.nombre_autor"
                  type="text"
                  class="mb-0 form-control"
                  id="floatingInput"
                  placeholder=""
                />
                <label label for="mb-0 floatingInput" class="text-secondary"
                  >Nombre del autor</label
                >
              </div>
            </b-col>
          </b-row>

          <b-row>
            <b-col>
              <div class="form-floating mb-4">
                <input
                  v-model="form.nombre_editorial"
                  type="text"
                  class="mb-0 form-control"
                  id="floatingInput"
                  placeholder=""
                />
                <label
                  label
                  for="mb-0 floatingInput"
                  class="mb-0 text-secondary"
                  >Nombre de la editorial</label
                >
              </div>
            </b-col>
          </b-row>

          <b-row>
            <b-col>
              <div class="form-floating">
                <select
                  class="mb-0 selector form-select"
                  id="floatingSelectGrid"
                  aria-label="Floating label select example"
                  v-model="form.nombre_categoria"
                >
                  <option selected>Seleccione una categoria</option>
                  <option value="Académico">Académico</option>
                  <option value="Digital">Digital</option>
                  <option value="Ilustración">Ilustración</option>
                  <option value="Manual">Manual</option>
                  <option value="Revista">Revista</option>
                </select>
                <label for="floatingSelectGrid">Categoria</label>
              </div>
            </b-col>
          </b-row>
        </b-container>

        <div class="mt-4 text-center">
          <b-button
            class="boton-modal-b mb-0"
            variant="danger"
            @click="$bvModal.hide(`modal-${index}`)"
            >Volver</b-button
          >
          <b-button
            type="submit"
            variant="success"
            class="boton-modal-a mb-0"
            @click="crear()"
            >Crear</b-button
          >
        </div>
      </b-form>
    </b-modal>
  </div>
</template>
<script>
import Swal from "sweetalert2";

export default {
  props: {
    articulo: {
      type: Object,
      default: () => {},
    },
    index: {
      type: Number,
      default: () => 1,
    },
  },
  data() {
    return {
      url: "https://bibliotech-conection.herokuapp.com/api/articulos/",
      form: {
        id: null,
        nombre: "",
        prestamo: "0",
        nombre_editorial: "",
        nombre_autor: "",
        nombre_categoria: "",
        isbn: "",
      },
    };
  },
  methods: {
    async crear() {
      Swal.fire({
        title: "¿Desea crear este nuevo articulo?",
        showDenyButton: true,
        confirmButtonText: "Sí",
        denyButtonText: `No`,
        confirmButtonColor: "#485eb2",
        denyButtonColor: "#ad0202",
        customClass: {
          actions: "my-actions",
          confirmButton: "order-3",
          denyButton: "order-2",
        },
      }).then((result) => {
        /* Read more about isConfirmed, isDenied below */
        if (result.isConfirmed) {
          this.axios.post(this.url, this.form).then((response) => {
            location.reload();
          });
        } else if (result.isDenied) {
          Swal.fire("No se guardo el articulo", "", "info");
        }
      });
    },
    async editItem() {
      console.log(this.articulo);
      (this.form.isbn = this.articulo.isbn),
        (this.form.nombre = this.articulo.nombre),
        (this.form.nombre_autor = this.articulo.nombre_autor),
        (this.form.nombre_editorial = this.articulo.nombre_editorial),
        (this.form.nombre_categoria = this.articulo.nombre_categoria);
    },
    async onSubmit(event) {
      event.preventDefault();
      console.log(JSON.stringify(this.form));
    },
  },
};
</script>
<style scoped>
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
.titulo-modal {
  font-family: "Roboto", sans-serif !important;
}
.boton-modal-a {
  background-color: #485eb2;
  border: none;
  margin-left: 12px;
}
.boton-modal-b {
  background-color: #ad0202;
  border: none;
}
.order-1 {
  order: 1;
}
.order-2 {
  order: 2;
}
.order-3 {
  order: 3;
}
</style>
