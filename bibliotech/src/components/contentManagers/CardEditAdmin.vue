<template>
  <div class="carta">
    <!-- Seccion superior de la carta -->
    <div class="carta-header">
      <div class="carta-header__texto">
        <p class="carta-header__texto carta-header__texto--titulo">
          {{ admin.nombre }}
        </p>
        <p class="carta-header__texto carta-header__texto--subtitulo">
          {{ admin.usuario }}
        </p>
      </div>
    </div>
    <!-- Seccion central de la carta -->
    <div class="carta-body">
      <div class="carta-body__imagen">
        <!-- <img src="../assets/images/placeholder.png"> -->
        <img src="../../assets/images/placeholder.png" alt="" />
      </div>
    </div>
    <!-- Seccion inferior de la carta -->
    <div class="carta-footer">
      <div class="carta-footer__botones">
        <a
          class="carta-footer__botones carta-footer__botones--cancelar"
          @click="borrar(admin.id)"
          >Borrar</a
        >
        <div>
          <b-button
            v-b-modal="`modal-admin-${index}`"
            @click="editAdmin()"
            class="carta-footer__botones carta-footer__botones--boton"
            >Editar</b-button
          >
          <b-modal
            class="titulo-modal"
            :id="`modal-admin-${index}`"
            :title="`Editando: ${form.nombre} ${form.apellido}`"
            hide-footer
          >
            <b-form @submit="onSubmit">
              <b-container>
                <b-row>
                  <b-col>
                    <div class="form-floating mt-4 mb-4">
                      <input
                        v-model="form.usuario"
                        type="text"
                        class="mb-0 form-control"
                        id="floatingInput"
                        placeholder=""
                      />
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
                        >Nombre de usuario</label
                      >
                    </div>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col>
                    <div class="form-floating mb-4">
                      <input
                        v-model="form.contraseña"
                        type="text"
                        class="mb-0 form-control"
                        id="floatingInput"
                        placeholder=""
                      />
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
                        >Contraseña</label
                      >
                    </div>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col>
                    <div class="form-floating mb-4">
                      <input
                        v-model="form.correo"
                        type="text"
                        class="mb-0 form-control"
                        id="floatingInput"
                        placeholder=""
                      />
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="text-secondary"
                        >Email</label
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
                        class="mb-0 text-secondary"
                        >Nombre</label
                      >
                    </div>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col>
                    <div class="form-floating">
                      <input
                        v-model="form.apellido"
                        type="text"
                        class="mb-0 form-control"
                        id="floatingInput"
                        placeholder=""
                      />
                      <label
                        label
                        for="mb-0 floatingInput"
                        class="mb-0 text-secondary"
                        >Apellido</label
                      >
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
                  @click="editar(form.id)"
                  >Editar</b-button
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
    admin: {
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
      url: "https://bibliotech-conection.herokuapp.com/api/",
      form: {
        id: "",
        nombre: "",
        apellido: "",
        contraseña: "",
        usuario: "",
        correo: "",
      },
    };
  },
  methods: {
    borrar(id) {
      console.log(id);
      Swal.fire({
        title: "¿Estas seguro?",
        text: "¡No podrás revertir esto!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#485eb2",
        cancelButtonColor: "#ad0202",
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
        }
      });
    },
    editAdmin() {
      console.log(this.admin);
      (this.form.id = this.admin.id),
        (this.form.nombre = this.admin.nombre),
        (this.form.apellido = this.admin.apellido),
        (this.form.contraseña = this.admin.contraseña),
        (this.form.usuario = this.admin.usuario),
        (this.form.correo = this.admin.correo);
    },
    editar(id) {
      console.log(id);
      Swal.fire({
        title: "¿Desea actualizar este usuario?",
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
            location.reload();
          });
        } else if (result.isDenied) {
          Swal.fire("No se guardo la informacion", "", "info");
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
