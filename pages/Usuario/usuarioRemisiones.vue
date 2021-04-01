<template>
  <v-card>
    <v-card-title>
      Remisiones
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Buscar"
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
    layout: 'usuario',
    data () {
      return {
        search: '',
        headers: [
          {
            text: 'Tipo de remisión',
            align: 'start',
            sortable: false,
            value: 'nombre',
          },
          { text: 'Número de orden', value: 'codigo' },
          { text: 'Fecha de remisión', value: 'Fecha' },
         
        ],
        desserts: [
          {
            nombre: 'Ortopedia',
            codigo: '36598',
            Fecha: '2021-10-10',
          },
          {
            nombre: 'Psicología',
            codigo: '98562',
            Fecha: '2021-05-01',
          },
          {
            nombre: 'Medicina interna',
            codigo: '632458',
            Fecha: '2021-03-15',
          },
          {
            nombre: 'Ortopedia',
            codigo: '968745',
            Fecha: '2021-11-10',
          },
          {
            nombre: 'Psicología',
            codigo: '521478',
            Fecha: '2021-06-01',
          },
          {
            nombre: 'Medicina interna',
            codigo: '96587',
            Fecha: '2021-02-14',
          },
        ],
      }
    },
  }
</script>