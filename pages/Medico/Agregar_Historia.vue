<template>
  <div>
    <h1>Agregar entrada a historia clinica</h1>
    <center>
      - Especialidad (Spinner) - Peso - Estatura - Descripcion - Examen (Boton+)
      - Medicamento (Boton+) - Receta (Boton+) - Remision (Boton+)

      <template>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-select
            v-model="Especialidad"
            :items="items"
            :rules="[v => !!v || 'Item is required']"
            label="Especialidad"
            required
          ></v-select>

          <v-text-field
            v-model="Peso"
            :rules="emailRules"
            label="Peso"
            required
          ></v-text-field>

          <v-text-field
            v-model="Estatura"
            :rules="emailRules"
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
              :rules="emailRules"
              label="Medicamento"
              required
            ></v-text-field>
            <v-btn elevation="2" fab small>
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-row>

          <v-row>
            <v-text-field
              v-model="Receta"
              :rules="emailRules"
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
              :rules="emailRules"
              label="Remision"
              required
            ></v-text-field>
            <v-btn elevation="2" fab small>
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-row>

          <v-checkbox
            v-model="checkbox"
            :rules="[v => !!v || 'You must agree to continue!']"
            label="Do you agree?"
            required
          ></v-checkbox>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
          >
            Validar
          </v-btn>

          <v-btn color="error" class="mr-4" @click="reset">
            Reiniciar
          </v-btn>

          <v-btn color="warning" @click="resetValidation">
            Reiniciar validacion
          </v-btn>
        </v-form>
      </template>
    </center>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+\..+/.test(v) || "E-mail must be valid"
    ],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false
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
