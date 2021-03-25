<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card style="width: 550px" elevation="12">
          <v-toolbar color="#3797a4">
            <v-card-title class="#0c354a--text">
              <center>Auxiliar - Medico</center>
            </v-card-title>
          </v-toolbar>
          <v-card-text>
            <v-card-text>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-text-field label="Nombres"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field label="Apellidos"></v-text-field>
                </v-col>
              </v-row>
              <v-text-field label="Cédula"></v-text-field>
              <v-row>
                <v-col cols="12" sm="4">
                  <v-text-field label="Fecha de Nacimiento"></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field label="Edad"></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field label="Sexo"></v-text-field>
                </v-col>
              </v-row>
              <v-select :items="especialidad" label="Especialidad"></v-select>
              <v-select :items="estado_civil" label="Estado civil"></v-select>
              <v-text-field label="Correo"></v-text-field>
              <v-text-field label="Teléfono"></v-text-field>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-select
                    :items="departamentos"
                    label="Departamento"
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select :items="ciudades" label="Ciudad"></v-select>
                </v-col>
              </v-row>
              <v-text-field label="Dirección"></v-text-field>
              <v-col>
                <center>
                  <v-btn class="white--text" color="#ee6f57">
                    Crear
                  </v-btn>
                </center>
              </v-col>
            </v-card-text>
          </v-card-text>
        </v-card>
      </v-col>

      <v-col>
        <v-card style="width: 550px" elevation="12">
          <v-toolbar color="#3797a4">
            <v-card-title class="#0c354a--text">
              <center>Paciente</center>
            </v-card-title>
            <v-spacer></v-spacer>
          </v-toolbar>
          <v-card-text>
            <v-card-text>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-text-field label="Nombres"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field label="Apellidos"></v-text-field>
                </v-col>
              </v-row>
              <v-text-field label="Cédula"></v-text-field>
              <v-row>
                <v-col cols="12" sm="4">
                  <v-text-field label="Fecha de Nacimiento"></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field label="Edad"></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field label="Sexo"></v-text-field>
                </v-col>
              </v-row>
              <v-text-field label="Ocupación"></v-text-field>
              <v-select :items="estado_civil" label="Estado civil"></v-select>
              <v-text-field label="Correo"></v-text-field>
              <v-text-field label="Teléfono"></v-text-field>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-select
                    :items="departamentos"
                    label="Departamento"
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select :items="ciudades" label="Ciudad"></v-select>
                </v-col>
              </v-row>
              <v-text-field label="Dirección"></v-text-field>
              <v-col>
                <center>
                  <v-btn class="white--text" color="#ee6f57">
                    Crear
                  </v-btn>
                </center>
              </v-col>
            </v-card-text>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-spacer></v-spacer>
    <v-container>
      <v-card>
        <v-card-title>
          <v-icon large left> </v-icon>

          <div>
            <strong class="#0c354a">Buscar Usuarios</strong>
          </div>
        </v-card-title>

        <v-toolbar flat color="transparent">
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Buscar Usuarios"
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
            <v-img :src="item.image" class="mr-4" max-width="64" min-width="64">
            </v-img>

            <v-list-item-content>
              <div v-text="item.rol"></div>
              <span
                class="text-uppercase font-weight-regular caption"
                v-text="item.nombre"
              ></span>
              <div v-text="item.documento"></div>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-card>
    </v-container>
  </v-container>
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
        image: "https://randomuser.me/api/portraits/women/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/women/20.jpg",
        nombre: "Yesenia Lopez Giraldo",
        documento: "1365478216",
        rol: "Auxiliar",
      },
      {
        image: "https://randomuser.me/api/portraits/women/30.jpg",
        nombre: "Maria Alejandra Franco Alzate",
        documento: "112365749",
        rol: "Medico",
      },
      {
        image: "https://randomuser.me/api/portraits/women/40.jpg",
        nombre: "Angie Rivera Hinestroza",
        documento: "114796632",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/women/50.jpg",
        nombre: "Dayana Mosquera Mosquera",
        documento: "974632114",
        rol: "Medico",
      },
      {
        image: "https://randomuser.me/api/portraits/women/60.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Auxiliar",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Medico",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
        rol: "Paciente",
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
        const text = item.documento.toLowerCase();

        return text.indexOf(search) > -1;
      });
    },
  },
};
</script>
