<template>
  <v-template>
    <center>
      <v-card style="width: 800px" elevation="12">
        <v-toolbar color="#3797a4">
          <v-card-title class="#0c354a--text">
            <center>Agregar medicamento</center>
          </v-card-title>
        </v-toolbar>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="nombre"
              :rules="rules.required"
              label="Nombre Medicamento"
              style="height: 100px"
              required
            ></v-text-field>
            <v-text-field
              v-model="descripcion"
              label="Descripcion"
              style="height: 100px"
            ></v-text-field>
            <center>
              <v-btn class="white--text" color="#ee6f57" @click="validate">
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
          Base de datos de Medicamentos
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
          :items="desserts"
          :search="search"
        ></v-data-table>
      </v-card>
    </v-container>
  </v-template>
</template>

<script>
export default {
  layout: "admin",
  data: () => ({
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },

    search: "",

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
    desserts: [
      {
        
        id: "111",
        nombre: "Acetaminofen",
        descripcion: "Analgesico",
      },
      {
        id: "222",
        nombre: "Loratadina",
        descripcion: "Antialergico",
      },
    ],
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
  },
};
</script>

<style>
</style>