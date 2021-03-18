<template>
  <div>
    <v-col>
      <v-row>
        <v-row>
          <v-list-item two-line>
            <v-avatar size="180">
              <v-img
                src="https://randomuser.me/api/portraits/women/21.jpg"
              ></v-img>
            </v-avatar>
            <span> Date &copy; {{ new Date().getFullYear()}}</span>
          </v-list-item>
        </v-row>

        <v-col>
          <v-text-field
            label="Nombres"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
          <v-text-field
            label="Apellidos"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
          <v-text-field label="Peso" disabled="isDisabled"></v-text-field>
        </v-col>

        <v-col>
          <v-text-field
            label="EStatura"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
          <v-text-field
            label="Telefono"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
          <v-text-field label="Direccion" disabled="isDisabled"> </v-text-field>
        </v-col>

        <v-col>
          <v-text-field
            label="Examenes"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
          <v-text-field
            label="Medicamentos"
            :rules="rules"
            hide-details="auto"
            disabled="isDisabled"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-textarea
          filled
          name="input-7-4"
          label="Filled textarea"
          value=""
          disabled=true
        >
        </v-textarea>

        <v-btn elevation="2">
          <v-icon
            >mdi-plus
            <label for="Ver mas informacion"></label>
          </v-icon>
        </v-btn>
      </v-row>
    </v-col>
  </div>
</template>

<script>
export default {
  layout: "medico",
  data: () => ({
    isDisabled: false
  })
};
</script>

<style></style>
