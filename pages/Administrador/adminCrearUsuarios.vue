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
            <v-form ref="formPersonalMedico" v-model="valid" lazy-validation>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="personal.nombre"
                    label="Nombre"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="personal.apellidos"
                    label="Apellidos"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-text-field
                v-model="personal.cedula"
                label="Cédula"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-row>
                <v-col cols="12" sm="4">
                  <v-menu
                    v-model="menu1"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    transition="scale-transition"
                    offset-y
                    min-width="auto"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="personal.fecha_nac"
                        label="Fecha de Nacimiento"
                        prepend-icon="mdi-calendar"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                      ></v-text-field>
                    </template>
                    <v-date-picker
                      v-model="personal.fecha_nac"
                      @input="menu1 = false"
                    ></v-date-picker>
                  </v-menu>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field
                    v-model="personal.edad"
                    label="Edad"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-select
                    v-model="personal.sexo"
                    :items="sexo"
                    label="Sexo"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-select
                    :items="especialidad"
                    v-model="personal.especialidad"
                    label="Especialidad"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select
                    :items="perfil"
                    v-model="personal.perfil"
                    label="Peril"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
              </v-row>

              <v-select
                :items="estado_civil"
                v-model="personal.estado_civil"
                label="Estado civil"
                :rules="rules.required"
                required
              ></v-select>
              <v-text-field
                v-model="personal.correo"
                label="Correo"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-text-field
                v-model="personal.telefono"
                label="Teléfono"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-select
                    v-model="personal.departamento"
                    :items="departamentos"
                    label="Departamento"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select
                    v-model="personal.ciudad"
                    :items="ciudades"
                    label="Ciudad"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
              </v-row>
              <v-text-field
                v-model="personal.direccion"
                label="Dirección"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-btn
                class="white--text"
                color="#ee6f57"
                @click="GuardarPersonal()"
              >
                Crear
              </v-btn>
            </v-form>
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
            <v-form ref="formPaciente" v-model="valid" lazy-validation>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="paciente.nombre"
                    label="Nombre"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-text-field
                    v-model="paciente.apellidos"
                    label="Apellidos"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-text-field
                v-model="paciente.cedula"
                label="Cédula"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-row>
                <v-col cols="12" sm="4">
                  <v-menu
                    v-model="menu2"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    transition="scale-transition"
                    offset-y
                    min-width="auto"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="paciente.fecha_nac"
                        label="Fecha de Nacimiento"
                        prepend-icon="mdi-calendar"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                      ></v-text-field>
                    </template>
                    <v-date-picker
                      v-model="paciente.fecha_nac"
                      @input="menu2 = false"
                    ></v-date-picker>
                  </v-menu>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-text-field
                    v-model="paciente.edad"
                    label="Edad"
                    :rules="rules.required"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="4">
                  <v-select
                    v-model="paciente.sexo"
                    :items="sexo"
                    label="Sexo"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
              </v-row>
              <v-text-field
                v-model="paciente.ocupacion"
                label="Ocupación"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-select
                :items="estado_civil"
                v-model="paciente.estado_civil"
                label="Estado civil"
                :rules="rules.required"
                required
              ></v-select>
              <v-text-field
                v-model="paciente.correo"
                label="Correo"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-text-field
                v-model="paciente.telefono"
                label="Teléfono"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-row>
                <v-col cols="12" sm="6">
                  <v-select
                    v-model="paciente.departamento"
                    :items="departamentos"
                    label="Departamento"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6">
                  <v-select
                    v-model="paciente.ciudad"
                    :items="ciudades"
                    label="Ciudad"
                    :rules="rules.required"
                    required
                  ></v-select>
                </v-col>
              </v-row>
              <v-text-field
                v-model="paciente.direccion"
                label="Dirección"
                :rules="rules.required"
                required
              ></v-text-field>
              <v-btn
                class="white--text"
                color="#ee6f57"
                @click="GuardarPaciente()"
              >
                Crear
              </v-btn>
            </v-form>
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
const url_apipaciente = "http://localhost:3001/pacientes/";
const url_apimedico = "http://localhost:3001/medicos/";
const url_apiauxiliar = "http://localhost:3001/auxiliares/";
export default {
  layout: "admin",
  data: () => ({
    date: new Date().toISOString().substr(0, 10),
    menu2: false,
    menu1: false,
    valid: true,
    sexo: ["Masculino", "Femenino"],
    estado_civil: ["Soltero", "Casado", "Divoriado", "Viudo"],
    departamentos: ["Antioquia", "Arauca", "Atlántico", "Bolívar"],
    ciudades: ["Medellín", "Bogotá", "Barranquilla", "Cartagena"],
    especialidad: ["a", "b", "c", "d"],
    perfil: ["Medico", "Auxiliar"],

    paciente: {
      nombre: "",
      apellidos: "",
      cedula: "",
      fecha_nac: new Date().toISOString().substr(0, 10),
      edad: "",
      sexo: "",
      ocupacion: "",
      estado_civil: "",
      correo: "",
      telefono: "",
      departamento: "",
      ciudad: "",
      direccion: "",
      perfil:"Paciente",
    },
    personal: {
      nombre: "",
      apellidos: "",
      cedula: "",
      fecha_nac: new Date().toISOString().substr(0, 10),
      edad: "",
      sexo: "",
      perfil: "",
      especialidad: "",
      estado_civil: "",
      correo: "",
      telefono: "",
      departamento: "",
      ciudad: "",
      direccion: "",
    },
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

    async GuardarPaciente() {
      if (this.$refs.formPaciente.validate()) {
        // Crear un nuevo objeto con la info del usuario
        try {
          let paciente = Object.assign({}, this.paciente);
          let response = await this.$axios.post(url_apipaciente, paciente);
          this.$swal.fire({
            type: "success",
            title: "Operación exitosa.",
            text: "El paciente se guardó correctamente.",
          });
        } catch (error) {
          console.log(error);
        }
      } else {
        this.$swal.fire({
          type: "warning",
          title: "Formulario incompleto.",
          text: "Hay campos que deben ser diligenciados.",
        });
      }
    },

    async GuardarPersonal() {
      if (this.$refs.formPersonalMedico.validate()) {
        if (this.personal.perfil == "Medico") {
          try {
            let medico = Object.assign({}, this.personal);
            let response = await this.$axios.post(url_apimedico, medico);
            this.$swal.fire({
              type: "success",
              title: "Operación exitosa.",
              text: "El medico se guardó correctamente.",
            });
          } catch (error) {
            console.log(error);
          }
        } else if (this.personal.perfil == "Auxiliar") {
          try {
            let auxiliar = Object.assign({}, this.personal);
            let response = await this.$axios.post(url_apiauxiliar, auxiliar);
            this.$swal.fire({
              type: "success",
              title: "Operación exitosa.",
              text: "El auxiliar se guardó correctamente.",
            });
          } catch (error) {
            console.log(error);
          }
        }
      } else {
        this.$swal.fire({
          type: "warning",
          title: "Formulario incompleto.",
          text: "Hay campos que deben ser diligenciados.",
        });
      }
    },

    DeletePaciente() {
      //Enviar una solicitud (Request) en un metodo delete
    },

    BuscarPaciente() {
      //Enviar una solicitud (Request) en un metodo get
    },

    ActualizarPaciente() {
      //Enviar una solicitud (Request) en un metodo update
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
