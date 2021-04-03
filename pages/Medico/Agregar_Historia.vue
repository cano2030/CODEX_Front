<template>
  <div>
    <h1>Agregar entrada a historia clinica</h1>
    <template>
      <v-form ref="formHistoria" v-model="valid" lazy-validation>
        <v-row>
          <v-menu
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="historia.fecha"
            transition="scale-transition"
            offset-y
            max-width="290px"
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-select
                v-model="historia.especialidad"
                :items="especializaciones"
                :rules="especialidadRules"
                label="Especialidad"
                required
              ></v-select>

              <v-text-field
                v-model="historia.fecha"
                solo-inverted
                hide-details
                label="Seleccionar fecha"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="historia.fecha" no-title scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="menu = false">
                Cancel
              </v-btn>
              <v-btn
                text
                color="primary"
                @click="$refs.menu.save(historia.fecha)"
              >
                OK
              </v-btn>
            </v-date-picker>
          </v-menu>
        </v-row>

        <v-select
          v-model="historia.cedula_medico"
          :items="cedula_medico"
          :rules="cedula_medicoRUles"
          label="cedula del medico que atiende"
          required
        ></v-select>

        <v-select
          v-model="historia.cedula_paciente"
          :items="cedula_paciente"
          :rules="cedula_pacienteRUles"
          label="cedula del paciente"
          required
        ></v-select>

        <v-text-field
          v-model="historia.peso"
          :rules="pesoRules"
          label="Peso"
          required
        ></v-text-field>

        <v-text-field
          v-model="historia.estatura"
          :rules="estaturaRules"
          label="Estatura"
          required
        ></v-text-field>
        <h3>Motivo de la consulta</h3>
        <v-textarea
          v-model="historia.motivo_consulta"
          filled
          text-color="accent"
          name="input-7-4"
          label="Acá es donde deberá ingresar, la razon por la que el paciente viene."
        ></v-textarea>
        <h3>Descripcion</h3>
        <v-textarea
          v-model="historia.descripcion"
          filled
          name="input-7-4"
          label="Acá es donde deberá ingresar el estado del paciente y todo lo que se relacione a ello."
        ></v-textarea>
        <!--         <template>
          <v-file-input
            v-model="historia.examen"
            label="File input"
            outlined
            multiple
            dense
          ></v-file-input>
        </template> -->

        <v-row>
          <v-text-field
            v-model="historia.medicamento"
            :rules="medicamentoRules"
            label="Medicamento"
            required
          ></v-text-field>
          <v-btn elevation="2" fab small>
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-row>

        <v-row>
          <v-text-field
            v-model="historia.posologia"
            :rules="posologiaRules"
            label="Receta"
            required
          ></v-text-field>
          <v-btn elevation="2" fab small>
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-row>

        <v-row>
          <v-text-field
            v-model="historia.remision"
            :rules="remisionRules"
            label="Remision"
            required
          ></v-text-field>
          <v-btn elevation="2" fab small>
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-row>

        <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="saveHistoria()"
         
        >
          Agregar
        </v-btn>

        <v-btn color="error" class="mr-4" @click="reset">
          Reiniciar
        </v-btn>

        <v-btn color="warning" @click="resetValidation">
          Reiniciar validacion
        </v-btn>
      </v-form>
    </template>
  </div>
</template>

<script>
export default {
  layout: "medico",
  data: () => ({
    valid: true,
    historia: {
      fecha: new Date().toISOString().substr(0, 10),
      especialidad: "",
      cedula_medico: "",
      cedula_paciente: "",
      peso: "",
      estatura: "",
      motivo_consulta: "",
      descripcion:"",
      //examen: "",
      medicamento: "",
      posologia: "",
      remision: "",
      id: ""
    },
    menu: "",

    idRules: [v => !!v || "Id must be valid"],
    cedula_medico: "",
    cedula_medicoRUles: [v => !!v || "La cedula del medico must be valid"],
    cedula_paciente: "",
    cedula_pacienteRUles: [v => !!v || "La cedula del paciente must be valid"],
    posologiaRules: [v => !!v || "Posologia must be valid"],
    especialidadRules: [v => !!v || "Especialidad is required"],
    pesoRules: [v => !!v || "Peso is required"],
    estaturaRules: [v => !!v || "Estatura is required"],
    medicamentoRules: [v => !!v || "Medicamento is required"],
    remisionRules: [v => !!v || "Remision is required"],
    select: null,
    especializaciones: [
      "Medicina general",
      "Odontología",
      "Ginecología",
      "Oftalmología",
      "Cirugía general",
      "Dermatología",
      "Ortopedía y traumatología"
    ],
    cedula_medico: ["111"],
    cedula_paciente: ["333", "444", "555", "666", "777", "888"]
  }),

  methods: {
    async saveHistoria() {
      if (this.$refs.formHistoria.validate()) {
        console.log("--Inicio guardar historia--");
        let historia = Object.assign({}, this.historia);
        //enviar una solicitud (Request) en un metodo post
        let response = await this.$axios.post(
          "http://localhost:3001/Historias_clinicas",
          historia
        );
        console.log(response);
      } else {
        console.log("Formulario incompleto");
      }
    },
    deleteHistoria() {
      //enviar una solicitud (Request) en un metodo delete
    },
    updateHistoria() {
      //enviar una solicitud (Request) en un metodo update
    },
    reset() {
      this.$refs.formHistoria.reset();
    },
    resetValidation() {
      this.$refs.formHistoria.resetValidation();
    }
  }
};
</script>

<style></style>
