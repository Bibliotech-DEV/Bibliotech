<template>
  <div class="contenedor-botonessuperiores">
    <!-- Boton para crear elementos -->
    <div v-b-modal.modal-creation class="boton__crear">
      <div class="icono-superior">
        <span class="mb-0 material-icons material-icons--boton-sup">add</span>
      </div>
    </div>
    <!-- FIN Boton para crear elementos -->

    <b-modal
      id="modal-creation"
      title="Nuevo Administrador"
      hide-footer
      centered
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
                <label label for="mb-0 floatingInput" class="text-secondary"
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
                <label label for="mb-0 floatingInput" class="text-secondary"
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
                <label label for="mb-0 floatingInput" class="text-secondary"
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
            @click="$bvModal.hide(`modal-creation`)"
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
    crear() {
      Swal.fire({
        title: "¿Desea crear este nuevo administrador?",
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
          Swal.fire("No se guardo el administrador", "", "info");
        }
      });
    },
    editAdmin() {
      console.log(this.admin);
      (this.form.usuario = this.admin.usuario),
        (this.form.contraseña = this.admin.contraseña),
        (this.form.correo = this.admin.correo),
        (this.form.nombre = this.admin.nombre),
        (this.form.apellido = this.admin.apellido);
    },
    onSubmit(event) {
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
