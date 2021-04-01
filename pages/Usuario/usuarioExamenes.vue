<template>
  <v-card>
    <v-card-title>
      Examenes
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Buscar"
        single-line
        hide-details
      >
      </v-text-field>
      <v-spacer></v-spacer>
     
    </v-card-title>

    <v-data-table :headers="headers" :items="desserts" :search="search">
      <template v-slot:[`item.actions`]="{}">
        <v-btn
          color="secondary"
          fab
          x-small
          dark
          href="https://www.ramajudicial.gov.co/documents/8957139/23136201/F-SST-04+Solicitud+de+Ex%C3%A1menes+M%C3%A9dicos+Ocupacionales+11-06-2019+V1.doc/74f5db35-26bf-4c10-ba02-84829bbc77b2"
          download
        >
          <v-icon>mdi-clipboard-edit-outline</v-icon>
        </v-btn>
      </template>
      <template>
        <v-btn
          color="secondary"
          fab
          x-small
          dark
          href="https://www.ramajudicial.gov.co/documents/8957139/23136201/F-SST-04+Solicitud+de+Ex%C3%A1menes+M%C3%A9dicos+Ocupacionales+11-06-2019+V1.doc/74f5db35-26bf-4c10-ba02-84829bbc77b2"
          download
        >
          <v-icon>mdi:clipboard-search-outline</v-icon>
        </v-btn>
      </template>
    </v-data-table>
  </v-card>
</template>


<script>
export default {
  layout: "usuario",

  data() {
    return {
      dialog: false,
      search: "",
      headers: [
        {
          text: "Examenes de Laboratorio",
          align: "start",
          sortable: false,
          value: "nombre",
        },
        { text: "Area de laboratorio", value: "area" },
        { text: "Orden del examen", value: "actions", sortable: false },
        { text: "fecha", value: "fecha" },
        { text: "Resultados", value: "actions", sortable: false },
        
      ],
      desserts: [
        {
          nombre: "Hemograma completo",
          area: "Hematología y coagulación",
          orden: 5,
          fecha: "12/11/2020",
          resultados: 4.0,
        },
        {
          nombre: "Perfil lipídico: Colesterol, LDL; HDL; triglicérido",
          area: "Químicas",
          orden: 9.0,
          fecha: "27/09/2020",
          resultados: 4.3,
        },
        {
          nombre: "Heces por parásito, sangre oculta",
          area: "Orina y heces",
          orden: 16.0,
          fecha: "06/18/2020",
          resultados: 6.0,
        },
        {
          nombre: "Perfil hepático: Bilirrubina, total y directa, AST, LDH",
          area: "Inmunología",
          orden: 3.7,
          fecha: "10/08/2019",
          resultados: 4.3,
        },
        {
          nombre: "Perfil triode: TSH, T3, T4",
          area: "Serología",
          orden: 16.0,
          fecha: "5/04/2020",
          resultados: 3.9,
        },
        {
          nombre: "Perfil hepático",
          area: "Microbiología",
          orden: 0.0,
          fecha: "19/02/2020",
          resultados: 0.0,
        },
        {
          nombre:
            "Panel básico metabólico: Electrolitos, glucosa, nitrógeno de urea,creatinina",
          area: "Citometría de flujo y biología molecular",
          orden: 0.2,
          fecha: "25/07/2020",
          resultados: 0,
        },
      ],
    };
  },
};
</script>

<style>
</style>