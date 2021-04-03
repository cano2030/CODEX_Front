<template>
  <v-card class="overflow-hidden">
    <v-toolbar flat>
      <v-toolbar-title class="#0c354a">Datos personales</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        class="white--text"
        color="#ee6f57"
        fab
        small
        @click="isEditing = !isEditing"
      >
        <v-icon v-if="isEditing"> mdi-close </v-icon>
        <v-icon v-else> mdi-pencil </v-icon>
      </v-btn>
    </v-toolbar>
    <v-card-text>
      <v-form ref="formUsuario" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field label="Nombres" disabled></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field label="Apellidos" disabled></v-text-field>
          </v-col>
        </v-row>
        <v-text-field label="Cédula" disabled></v-text-field>
        <v-row>
          <v-col cols="12" sm="4">
            <v-text-field label="Fecha de Nacimiento" disabled></v-text-field>
          </v-col>
          <v-col cols="12" sm="4">
            <v-text-field label="Edad" disabled></v-text-field>
          </v-col>
          <v-col cols="12" sm="4">
            <v-text-field label="Sexo" disabled></v-text-field>
          </v-col>
        </v-row>
        <!--DATOS QUE SE PUEDEN ACTUALIZAR -->
        <v-text-field
          v-model="usuario.ocupacion"
          label="Ocupación"
          :rules="rules.required"
          :disabled="!isEditing"
        ></v-text-field>
        <v-select
          v-model="usuario.estado_civil"
          :items="estado_civil"
          label="Estado civil"
          :rules="rules.required"
          :disabled="!isEditing"
        ></v-select>
        <v-text-field
          v-model="usuario.correo"
          label="Correo"
          :rules="rules.required"
          :disabled="!isEditing"
        ></v-text-field>
        <v-text-field
          v-model="usuario.telefono"
          label="Teléfono"
          :rules="rules.required"
          :disabled="!isEditing"
        ></v-text-field>
        <v-row>
          <v-col cols="12" sm="6">
            <v-select
              v-model="usuario.departamento"
              :items="departamentos"
              label="Departamento"
              :rules="rules.required"
              :disabled="!isEditing"
            ></v-select>
          </v-col>
          <v-col cols="12" sm="6">
            <v-select
              v-model="usuario.ciudad"
              :items="ciudades"
              label="Ciudad"
              :rules="rules.required"
              :disabled="!isEditing"
            ></v-select>
          </v-col>
        </v-row>
        <v-text-field
          v-model="usuario.direccion"
          :disabled="!isEditing"
          label="Dirección"
          :rules="rules.required"
        ></v-text-field>
      </v-form>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        class="white--text"
        :disabled="!isEditing"
        color="#ee6f57"
        @click="updateUser"
      >
        Guardar
      </v-btn>
    </v-card-actions>
    <v-snackbar v-model="hasSaved" :timeout="2000" absolute bottom left>
      Datos actualizados!
    </v-snackbar>
  </v-card>
</template>


<script>
export default {
  layout: "usuario",
  async asyncData({ params }) {
    let id_usuario = params.id;
    return { id_usuario };
  },
  data: () => ({
    valid: true,
    hasSaved: false,
    isEditing: null,
    model: null,
    usuario: {},
    estado_civil: ["Soltero", "Casado", "Divorciado", "Viudo"],
    departamentos: ["Antioquia", "Arauca", "Atrlántico", "Bolívar"],
    //ciudades: ["Medellín", "Bogotá", "Barranquilla", "Cartagena"],
    ciudades: [],
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
  }),

  beforeMount() {
    this.getUsuario();
  },

  methods: {
    async getUsuario() {
      try {
        //
        let response = await this.$axios.get(
          "http://localhost:3001/Usuario/usuarioPerfil" + this.id_usuario
        );
        this.usuario = response.data;
      } catch (error) {
        this.$swal
          .fire({
            type: "error",
            title: "Oops...",
            text: "El usuario no existe o hubo un error cargandolo.",
            allowEscapeKey: false,
            allowOutsideClick: false,
          })
          .then((result) => {
            if (result.value) {
              this.$router.push("/Usuario/usuarioPerfil");
            }
          });
      }
    },
    async getCiudades() {
      try {
        let response = await this.$axios.get(
          "http://localhost:3000/Usuario/usuarioPerfil"
        );
        this.ciudades = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
<style>
</style>