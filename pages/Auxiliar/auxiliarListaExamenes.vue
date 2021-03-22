<template>
  <v-card>
    <v-card-title>
      Examenes del paciente
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
      <v-layout row justify-center>
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on }">
        <v-btn color="primary" dark v-on="on">Open Dialog</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">User Profile</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm6 md4>
                <v-text-field label="Legal first name*" required></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field label="Legal middle name" hint="example of helper text only on focus"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field
                  label="Legal last name*"
                  hint="example of persistent helper text"
                  persistent-hint
                  required
                ></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-text-field label="Email*" required></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-text-field label="Password*" type="password" required></v-text-field>
              </v-flex>
              <v-flex xs12 sm6>
                <v-select
                  :items="['0-17', '18-29', '30-54', '54+']"
                  label="Age*"
                  required
                ></v-select>
              </v-flex>
              <v-flex xs12 sm6>
                <v-autocomplete
                  :items="['Skiing', 'Ice hockey', 'Soccer', 'Basketball', 'Hockey', 'Reading', 'Writing', 'Coding', 'Basejump']"
                  label="Interests"
                  multiple
                ></v-autocomplete>
              </v-flex>
            </v-layout>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
          <v-btn color="blue darken-1" flat @click="dialog = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="desserts"
      :search="search"
    ></v-data-table>
  </v-card>
</template>


<script>
  export default {
    layout: 'auxiliar',
    data: () => ({
      dialog: false
    }),
    
    data () {
      return {
        search: '',
        headers: [
          {
            text: 'Examenes de Laboratorio',
            align: 'start',
            sortable: false,
            value: 'nombre',
          },
          { text: 'Area de laboratorio', value: 'area' },
          { text: 'Orden del examen', value: 'orden' },
          { text: 'fecha', value: 'fecha' },
          { text: 'Resultados', value: 'resultados' },
         
        ],
        desserts: [
          {
            nombre: 'Frozen Yogurt',
            area: 'Hematología y coagulación',
            orden: 6.0,
            fecha: 24,
            resultados: 4.0,
          },
          {
            nombre: 'Ice cream sandwich',
            area: 'Químicas',
            orden: 9.0,
            fecha: 37,
            resultados: 4.3,
          },
          {
            nombre: 'Eclair',
            area: 'Orina y heces',
            orden: 16.0,
            fecha: 23,
            resultados: 6.0,
          },
          {
            nombre: 'Cupcake',
            area: 'Inmunología',
            orden: 3.7,
            fecha: 67,
            resultados: 4.3,
          },
          {
            nombre: 'Gingerbread',
            area: 'Serología',
            orden: 16.0,
            fecha: 49,
            resultados: 3.9,
          },
          {
            nombre: 'Jelly bean',
            area: 'Microbiología',
            orden: 0.0,
            fecha: 94,
            resultados: 0.0,
          },
          {
            nombre: 'Lollipop',
            area: 'Citometría de flujo y biología molecular',
            orden: 0.2,
            fecha: 98,
            resultados: 0,
          },
          {
            nombre: 'Honeycomb',
            area: 408,
            orden: 3.2,
            fecha: 87,
            resultados: 6.5,
          },
          {
            nombre: 'Donut',
            area: 452,
            orden: 25.0,
            fecha: 51,
            resultados: 4.9,
          },
          {
            nombre: 'KitKat',
            area: 518,
            orden: 26.0,
            fecha: 65,
            resultados: 7,
          },
        ],
      }
    },
  
  }
</script>

<style>

</style>