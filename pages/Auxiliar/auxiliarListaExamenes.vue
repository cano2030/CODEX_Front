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