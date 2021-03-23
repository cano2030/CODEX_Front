<template>
  <v-template>
    <center>
      <v-card style="width: 800px" elevation="12">
        <v-toolbar color="#a4ebf3">
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
              <v-btn class="white--text" color="#ff5722" @click="validate">
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
          <v-icon large left> </v-icon>

          <div>
            <strong class="#0c354a">Buscar Medicamento</strong>
          </div>
        </v-card-title>

        <v-toolbar flat color="transparent">
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Buscar medicamento"
            single-line
          ></v-text-field>
        </v-toolbar>

        <v-list three-line color="#f4f9f9">
          <v-list-item
            v-for="(item, i) in searching"
            :key="i"
            ripple
            @click="() => {}"
          >
            <v-list-item-content>
              <div v-text="item.id"></div>
              <div v-text="item.nombre"></div>
              <span
                class="text-uppercase font-weight-regular caption"
                v-text="item.descripcion"
              ></span>
            </v-list-item-content>
          </v-list-item>
        </v-list>
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
    items: [
      {
        nombre: "Acetaminofen",
        id: "111",
        descripcion: "analgesico",
      },
      {
        nombre: "Loratadina",
        id: "222",
        descripcion: "Antialergico",
      },
    ],
    search: "",
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
  },
  computed: {
    searching() {
      if (!this.search) return this.items;

      const search = this.search.toLowerCase();

      return this.items.filter((item) => {
        const text = item.id.toLowerCase();

        return text.indexOf(search) > -1;
      });
    },
  },
};
</script>

<style>
</style>