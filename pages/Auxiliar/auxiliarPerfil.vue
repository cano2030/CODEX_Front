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
      <v-row>
        <v-col cols="12" sm="6">
          <v-text-field 
          value="Karen Johana"
          label="Nombres" disabled="isDisabled"></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-text-field 
           value="Mosquera Mosquera"
          label="Apellidos" disabled="isDisabled"></v-text-field>
        </v-col>
      </v-row>
      <v-text-field  value="1478523699" label="Cédula" disabled="isDisabled"></v-text-field>
      <v-row>
        <v-col cols="12" sm="4">
          <v-text-field
           value="15/07/1995"
            label="Fecha de Nacimiento"
            disabled="isDisabled"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="4">
          <v-text-field value="25" label="Edad" disabled="isDisabled"></v-text-field>
        </v-col>
        <v-col cols="12" sm="4">
          <v-text-field value="Femenino" label="Sexo" disabled="isDisabled"></v-text-field>
        </v-col>
      </v-row>
      <v-text-field value="Auxiliar de Enfermería" label="Ocupación" :disabled="!isEditing"></v-text-field>
      <v-select value="Soltero" :items="estado_civil" label="Estado civil" :disabled="!isEditing"></v-select>
      <v-text-field value="karenmosquera25@gmail.com" label="Correo" :disabled="!isEditing"></v-text-field>
      <v-text-field value="3147853644" label="Teléfono" :disabled="!isEditing"></v-text-field>
      <v-row>
        <v-col cols="12" sm="6">
          <v-select value="Antioquia" :items="departamentos" label="Departamento" :disabled="!isEditing"></v-select>
        </v-col>
        <v-col cols="12" sm="6">
          <v-select value="Medellín" :items="ciudades" label="Ciudad" :disabled="!isEditing"></v-select>
        </v-col>
      </v-row>
      <v-text-field value="cr 27a # 56-47" :disabled="!isEditing" label="Dirección"></v-text-field>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        class="white--text"
        :disabled="!isEditing"
        color="#ee6f57"
        @click="save"
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
  layout: "auxiliar",
  data() {
    return {
      hasSaved: false,
      isEditing: null,
      model: null,
      estado_civil: ["Soltero", "Casado", "Divorciado", "Viudo"],
      departamentos: ["Antioquia", "Arauca", "Atrlántico", "Bolívar"],
      ciudades: ["Medellín", "Bogotá", "Barranquilla", "Cartagena"],
    };
  },
  isDisabled: false,

  methods: {
    save() {
      this.isEditing = !this.isEditing;
      this.hasSaved = true;
    },
  },
};
</script>
<style>
</style>