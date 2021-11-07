<template>
  <div class="carta">
    <!-- Seccion superior de la carta -->
    <div class="carta-header">
      <div class="carta-header__texto">
        <p class="carta-header__texto carta-header__texto--titulo">
          {{ articulo.nombre }}
        </p>
        <p class="carta-header__texto carta-header__texto--subtitulo">
          {{ articulo.nombre_autor }}
        </p>
      </div>
    </div>
    <!-- Seccion central de la carta -->
    <div class="carta-body">
      <div class="carta-body__imagen">
        <!-- <img src="../assets/images/placeholder.png"> 
              <img :src="`cardImage/${item.image}`" alt="">-->
        <img src="../../assets/images/placeholder.png" />
      </div>
    </div>
    <!-- Seccion inferior de la carta -->
    <div class="carta-footer">
      <div class="carta-footer__botones">
        <a
          class="carta-footer__botones carta-footer__botones--cancelar"
          @click="borrar(articulo.id)"
          >Borrar</a
        >
        <!-- <input class="carta-footer__botones carta-footer__botones--boton" type="submit"
            value="EDITAR" > -->
        <div>
          <b-button
            v-b-modal="`modal-item-${index}`"
            @click="editItem()"
            class="carta-footer__botones carta-footer__botones--boton"
            >Editar</b-button
          >
          <b-modal
            class="titulo-modal"
            :id="`modal-item-${index}`"
            :title="`Editando: ${form.nombre}`"
            hide-footer
            centered
          >
            <!-- <p class="my-4">{{item}}</p> -->
            <b-form @submit="onSubmit">
              <!--
                <b-form-group id="input-group-2" label="Nombre:" label-for="input-2">
                  <b-form-input
                    id="input-2"
                    v-model="form.book_title"
                    placeholder="Enter name"
                    required
                  ></b-form-input>
                </b-form-group> -->

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
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
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
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
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
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
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
                  @click="cerrarModal()"
                  >Cancelar</b-button
                >
                <b-button
                  type="submit"
                  variant="success"
                  class="boton-modal-a mb-0"
                  @click="editar(form.id)"
                  >Actualizar</b-button
                >
              </div>
            </b-form>
          </b-modal>
        </div>
      </div>
    </div>
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
        id: "",
        nombre: "",
        prestamo: "",
        nombre_editorial: "",
        nombre_autor: "",
        nombre_categoria: "",
        isbn: "",
      },
    };
  },
  methods: {
    pushLogin() {
      this.$router.push("Login");
    },
    cerrarModal() {
      this.$bvModal.hide(`modal-item-${this.index}`);
    },
    editItem() {
      (this.form.id = this.articulo.id),
        (this.form.isbn = this.articulo.isbn),
        (this.form.nombre = this.articulo.nombre),
        (this.form.nombre_autor = this.articulo.nombre_autor),
        (this.form.nombre_editorial = this.articulo.nombre_editorial),
        (this.form.nombre_categoria = this.articulo.nombre_categoria);
    },
    editar(id) {
      console.log(id);
      Swal.fire({
        title: "¿Desea actualizar este articulo?",
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
          this.axios.put(this.url + id, this.form).then((response) => {
            this.cerrarModal();
            this.pushLogin();
          });
        } else if (result.isDenied) {
          Swal.fire("No se guardo la informacion", "", "info");
        }
      });
    },
    borrar(id) {
      console.log(id);
      Swal.fire({
        title: "¿Esta seguro?",
        text: "¡No podrás revertir esto!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#485eb2",
        cancelButtonColor: "#ad0202",
        cancelButtonText: "Cancelar",
        confirmButtonText: "Si, eliminalo!",
        customClass: {
          actions: "my-actions",
          confirmButton: "order-3",
          cancelButton: "order-2",
        },
      }).then((result) => {
        if (result.isConfirmed) {
          this.axios.delete(this.url + id).then((response) => {
            location.reload();
          });
        } else {
          Swal.close();
        }
      });
    },
    onSubmit(event) {
      event.preventDefault();
      console.log(JSON.stringify(this.form));
    },
  },
};
</script>
<style scoped>
.carta {
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  max-width: 316px;
  min-width: 286px;
  width: 20vw;
  height: 280px;
  border-radius: 7px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  box-sizing: border-box;
  margin-top: 2px;
}
.carta-header {
  height: 68px;
  display: flex;
  align-items: center;
}
.carta-header__texto {
  height: 42px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 1rem;
  box-sizing: border-box;
}
.carta-header__texto--titulo {
  font-family: "Roboto";
  font-size: 1rem;
  font-weight: 500;
  padding: 0%;
  margin: 0%;
}
.carta-header__texto--subtitulo {
  font-family: "Roboto";
  font-size: 0.8rem;
  font-weight: 300;
  padding: 0%;
  margin: 0%;
}
.carta-body {
  background-color: #e6e6e6;

  height: 178px;
  display: flex;
  justify-content: center;
}
.carta-body__imagen {
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
  max-height: 174px;
  width: 100%;
  box-sizing: border-box;
}
.carta-body img {
  height: auto;
}
.carta-footer {
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
}
.carta-footer__botones {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.carta-footer__botones--cancelar {
  font-family: "Roboto", sans-serif;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 400;
  color: #ffffff;
  text-decoration: none;
  background-color: #ad0202;
  padding: 5px;
  border: none;
  outline: none;
  cursor: pointer;
  margin-right: 6px;
}
.carta-footer__botones--cancelar:hover {
  background-color: #8f0303;
}
.carta-footer__botones--boton {
  font-family: "Roboto", sans-serif;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 400;
  color: #ffffff;
  background-color: #485eb2;
  padding: 5px;
  border: none;
  outline: none;
  cursor: pointer;
}
.carta-footer__botones--boton:hover {
  background-color: #3f529c;
}
.titulo-modal {
  font-family: "Roboto", sans-serif !important;
}
.boton-modal-a {
  background-color: #485eb2;
  border: none;
  margin-left: 12px;
  padding-top: 5px !important;
}
.boton-modal-b {
  background-color: #ad0202;
  border: none;
  padding-top: 5px !important;
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
