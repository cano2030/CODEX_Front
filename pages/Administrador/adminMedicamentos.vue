<template>
  <v-template>
    <center>
      <v-card style="width: 800px" elevation="12">
        <v-toolbar color="#3797a4">
          <v-card-title class="#0c354a--text">
            <center>Agregar medicamentos</center>
          </v-card-title>
        </v-toolbar>
        <v-card-text>
          <v-form ref="formMedicamentos" v-model="valid" lazy-validation>
            <v-text-field
              v-model="CamposMedicamento.nombre"
              :rules="rules.required"
              label="Nombre Medicamento"
              style="height: 100px"
              required
            ></v-text-field>
            <v-text-field
              v-model="CamposMedicamento.descripcion"
              label="Descripcion"
              style="height: 100px"
            ></v-text-field>
            <center>
              <v-btn class="white--text" color="#ee6f57" @click="agregarMedicamento()">
                Agregar
              </v-btn>
              
            </center>
          </v-form>
        </v-card-text>
      </v-card>
    </center>
    <v-container>
      <v-card>
        <v-card-title>
          Base de datos de medicamentos
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
          :items="medicamento"
          :search="search"
        ></v-data-table>
      </v-card>
    </v-container>
  </v-template>
</template>

<script>
const url_apimedicamento = "http://localhost:3001/medicamentos/";
export default {
  beforeMount() {
    //this.loadUser();
    this.getMedicamentos();
  },
  layout: "admin",
  data: () => ({
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
    search: "",
    medicamento: [],

    CamposMedicamemto: {
      nombre: "",
      descripcion:"",
    },

    headers: [
      {
        text: "Nombre del medicamento",
        align: "start",
        sortable: false,
        value: "nombre",
      },
      { text: "ID", value: "id" },
      { text: "Descripcion", value: "descripcion" },
    ],
    
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    resetForm () {
      this.CamposMedicamemto.nombre = ''
      this.CamposMedicamemto.descripcion = ''
      
    },
    async getMedicamentos() {
      try {
        let response = await this.$axios.get(url_apimedicamento);
        this.medicamento = response.data;
        
      } catch (error) {
        console.error(error);
      }
    },
    async agregarMedicamento() {
      if (this.$refs.formMedicamento.validate()) {
        
        // Crear un nuevo objeto con la info del usuario
        try {
          let medicamento = Object.assign({}, this.CamposMedicamemto);
          let response = await this.$axios.post(url_apimedicamento, medicamento);
          this.$swal.fire({
            type: "success",
            title: "Operación exitosa.",
            text: "El medicamento se guardó correctamente.",
          });
        } catch (error) {
          console.log(error);
        }
        this.resetForm();
        
        this.getMedicamentos();
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