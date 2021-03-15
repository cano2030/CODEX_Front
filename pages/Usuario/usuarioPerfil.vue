<template>
  <div>
    <h1>Datos personales</h1>
    <template>
      <div>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              label="Nombres"
              :rules="rules"
              hide-details="auto"
              disabled="isDisabled"
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              label="Apellidos"
              :rules="rules"
              hide-details="auto"
              disabled="isDisabled"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-text-field label="Cédula" disabled="isDisabled"></v-text-field>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              label="Fecha de nacimiento"
              disabled="isDisabled"
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field label="Edad" disabled="isDisabled"></v-text-field>
          </v-col>
        </v-row>
        <v-text-field label="Teléfono" disabled="isDisabled"></v-text-field>
        <v-text-field label="Dirección" disabled="isDisabled"></v-text-field>
      </div>
    </template>
    <template>
      <v-row align="center" justify="space-around">
        <v-btn tile color="success">
          <v-icon left> mdi-pencil </v-icon>
          Actualizar datos
        </v-btn>
      </v-row>
    </template>
  </div>
</template>
</div>
</template>

<script>
export default {
  layout: "usuario",
  data: () => ({
    isDisabled: false,
  }),
};
</script>