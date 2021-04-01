<template>
    <div>
      <h1>Agregar entrada a historia clinica</h1>
      <template>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-select
            v-model="Especialidad"
            :items="especializaciones"
            :rules="especialidadRules"
            label="Especialidad"
            required
          ></v-select>

          <v-text-field
            v-model="Peso"
            :rules="pesoRules"
            label="Peso"
            required
          ></v-text-field>

          <v-text-field
            v-model="Estatura"
            :rules="estaturaRules"
            label="Estatura"
            required
          ></v-text-field>

          <v-textarea
            filled
            name="input-7-4"
            label="Filled textarea"
            value="Aca es donde debera ingresar, algo que necesite ser descrito relacionado al estado del paciente."
          ></v-textarea>

          <template>
            <v-file-input
              label="File input"
              outlined
              multiple
              dense
            ></v-file-input>
          </template>

          <v-row>
            <v-text-field
              v-model="Medicamento"
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
              v-model="Posologia"
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
              v-model="Remision"
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
            @click="validate"
            text
            to="/Medico/Historia_clinica"
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
    posologia: "",
    posologiaRules: [v => /.+@.+\..+/.test(v) || "Posologia must be valid"],
    especialidad: "",
    especialidadRules: [v => !!v || "Especialidad is required"],
    peso: "",
    pesoRules: [v => !!v || "Peso is required"],
    estatura: "",
    estaturaRules: [v => !!v || "Estatura is required"],
    medicamento: "",
    medicamentoRules: [v => !!v || "Medicamento is required"],
    remision: "",
    remisionRules: [v => !!v || "Remision is required"],
    select: null,
    especializaciones: [
      "Medicina general",
      "Odontología",
      "Ginecología",
      "Oftalmología",
      "Cirugía general",
      "Dermatología",
      "Ortopedía y traumatología",
    ],
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>

<style></style>
