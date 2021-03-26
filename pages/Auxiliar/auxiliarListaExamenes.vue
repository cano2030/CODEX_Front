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
      <v-spacer>
        <div>
          <v-row justify="center">
            <v-dialog v-model="dialog" persistent max-width="600px">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  justify="center"
                  class="white--text"
                  color="#ee6f57"
                  fab
                  small
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon> mdi-clipboard-plus-outline </v-icon>
                </v-btn>
              </template>
              <v-card>
                <v-card-title>
                  <span class="headline">Añadir nuevo examen</span>
                </v-card-title>
                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col cols="12" sm="6" md="4">
                        <v-text-field
                          label="Numero de Identificación"
                          required
                          :disabled="true"
                          value="1000439971"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="6" md="4">
                        <v-text-field
                          label="Nombre"
                          :disabled="true"
                          value="Mariana "
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="6" md="4">
                        <v-text-field
                          label="Apellidos"
                          persistent-hint
                          required
                          :disabled="true"
                          value="Palacios Hinestroza"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="6">
                        <v-select
                          :items="[
                            'Hematología y coagulación',
                            'Químicas',
                            'Orina y heces',
                            'Inmunología',
                            'Serología',
                            '	Microbiología',
                            'Citometría de flujo y biología molecular',
                          ]"
                          label="Area de laboratorio"
                          required
                        ></v-select>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Nombre del examen"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-file-input
                          accept="image/*"
                          label="Archivo de la orden"
                        ></v-file-input>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="dialog = false">
                    Close
                  </v-btn>
                  <v-btn color="blue darken-1" text @click="dialog = false">
                    Save
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-row>
        </div>
      </v-spacer>
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
  layout: "auxiliar",

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