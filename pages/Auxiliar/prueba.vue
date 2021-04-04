<template>
  <v-template>
    <center>
      <v-card style="width: 800px" elevation="12">
        <v-toolbar color="#3797a4">
          <v-card-title class="#0c354a--text">
            <center>Agregar especialidad</center>
          </v-card-title>
        </v-toolbar>
        <v-card-text>
          <v-form ref="formEspecialidad" v-model="valid" lazy-validation>
            <v-text-field
              v-model="CamposEspecialidad.nombre"
              :rules="rules.required"
              label="Nombre Especialidad"
              style="height: 100px"
              required
            ></v-text-field>
            <v-text-field
              v-model="CamposEspecialidad.descripcion"
              label="Descripcion"
              style="height: 100px"
            ></v-text-field>
            <center>
              <v-btn
                class="white--text"
                color="#ee6f57"
                @click="agregarEspecialidad()"
              >
                Agregar
              </v-btn>
              <v-btn
                color="#0c354a"
                class="ma-1"
                v-bind="attrs"
                v-on="on"
                plain
              >
                Eliminar
              </v-btn>
            </center>
          </v-form>
        </v-card-text>
      </v-card>
    </center>
    <v-container>
      <v-card>
        <v-card-title>
          Base de datos de Especialidades
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Buscar"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="especialidad"
          :search="search"
        ></v-data-table>
      </v-card>
    </v-container>
  </v-template>
</template>

<script>
const url_apiespec = "http://localhost:3001/especialidades/";
export default {
  beforeMount() {
    //this.loadUser();
    this.getEspecilidad();
  },
  layout: "admin",
  data: () => ({
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
    search: "",

    headers: [
      {
        text: "Id",
        align: "start",
        value: "id",
      },
      { text: "Nombre de la especialidad", value: "nombre" },
      { text: "Descripcion", value: "descripcion" },
    ],
    especialidad: [],

    CamposEspecialidad: {
      nombre: "",
      descripcion:"",
    },
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },

    async getEspecilidad() {
      try {
        let response = await this.$axios.get(url_apiespec);
        this.especialidad = response.data;
        
      } catch (error) {
        console.error(error);
      }
    },

    async agregarEspecialidad() {
      if (this.$refs.formEspecialidad.validate()) {
        
        // Crear un nuevo objeto con la info del usuario
        try {
          let especialidad = Object.assign({}, this.CamposEspecialidad);
          let response = await this.$axios.post(url_apiespec, especialidad);
          this.$swal.fire({
            type: "success",
            title: "Operación exitosa.",
            text: "El examen se guardó correctamente.",
          });
        } catch (error) {
          console.log(error);
        }

        
        this.getEspecilidad();
      } else {
        this.$swal.fire({
          type: "warning",
          title: "Formulario incompleto.",
          text: "Hay campos que deben ser diligenciados.",
        });
      }
    },
  },
};
</script>

<style>
</style>