<template>
  <v-container fluid>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page.sync="page"
      hide-default-footer
    >
      <template v-slot:header>
        <v-toolbar class="mb-2" color="#3797a4" dark flat>
          <v-row>
            <v-col cols="12" sm="5">
              <v-select
                prepend-inner-icon="mdi-magnify"
                solo-inverted
                hide-details
                :items="especializaciones"
                label="Buscar por especialización"
                @change="filterEspecializacion"
                v-model="especializacion_seleccionada"
              ></v-select>
            </v-col>
            <v-col cols="12" sm="5">
              <v-menu
                ref="menu"
                v-model="menu"
                :close-on-content-click="false"
                :return-value.sync="date"
                transition="scale-transition"
                offset-y
                max-width="290px"
                min-width="auto"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="date"
                      solo-inverted
                      hide-details
                      label="Buscar por fecha"
                      prepend-inner-icon="mdi-calendar"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker @change="filterMes" v-model="date" type="month" no-title scrollable>
                  <v-spacer></v-spacer>
                  <v-btn text color="primary" @click="menu = false">
                    Cancel
                  </v-btn>
                  <v-btn text color="primary" @click="$refs.menu.save(date)">
                    OK
                  </v-btn>
                </v-date-picker>
              </v-menu>
            </v-col>
            <v-col cols="12" sm="2" justify="center" align="center">
              <v-btn class="text-center" small color="#ee6f57" dark @click="limpiarFiltros">
                Limpiar filtros
              </v-btn>
            </v-col>
          </v-row>
        </v-toolbar>
      </template>

      <template v-slot:default="props">
        <v-row>
          <v-col v-for="item in props.items" :key="item.especializacion" cols="12">
            <v-card>
              <v-card-title class="subheading font-weight-bold">
                <!--<v-btn class="mx-2" fab dark small color="primary">
                  <v-icon dark> mdi-share </v-icon>
                </v-btn>-->
                {{ item.especializacion }}
              </v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item>
                  <v-list-item-content>Número de historia:</v-list-item-content>
                  <v-list-item-content class="align-end">
                    {{ item.num_historia }}
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-content>Fecha:</v-list-item-content>
                  <v-list-item-content class="align-end">
                    {{ item.fecha }}
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-content>Motivo de consulta:</v-list-item-content>
                  <v-list-item-content class="align-end">
                    {{ item.motivo_consulta }}
                  </v-list-item-content>
                </v-list-item>

                <v-list-item>
                  <v-list-item-content>Descripción:</v-list-item-content>
                  <v-list-item-content class="align-end">
                    {{ item.descripcion }}
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>

      <template v-slot:footer>
        <v-row class="mt-2" align="center" justify="center">
          <v-spacer></v-spacer>
          <span class="mr-4 grey--text">
            Page {{ page }} of {{ numberOfPages }}
          </span>
          <v-btn
            fab
            dark
            color="#3797a4"
            class="mr-1"
            @click="formerPage"
          >
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn fab dark color="#3797a4" class="ml-1" @click="nextPage">
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
export default {
  layout: "usuario",
  beforeMount() {
    this.items = this.historias;
  },
  data: () => ({
    date: new Date().toISOString().substr(0, 7),
    menu: false,
    page: 1,
    itemsPerPage: 3,
    especializacion_seleccionada: null,
    filter: {},
    especializaciones: [
      "Medicina general",
      "Odontología",
      "Ginecología",
      "Oftalmología",
      "Cirugía general",
      "Dermatología",
      "Ortopedía y traumatología",
    ],
    headers: [],
    items: [],
    historias: [
      {
        especializacion: "Medicina general",
        num_historia: "23659",
        fecha: "2021-03-18",
        motivo_consulta: "Fiebre",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        especializacion: "Odontología",
        num_historia: "36985",
        fecha: "2021-11-02",
        motivo_consulta: "Carie",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        especializacion: "Dermatología",
        num_historia: "8547",
        fecha: "2021-09-10",
        motivo_consulta: "Grano",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        especializacion: "Oftalmología",
        num_historia: "123",
        fecha: "2020-03-01",
        motivo_consulta: "Ciego",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
    ],
  }),
  computed: {
    numberOfPages() {
      return Math.ceil(this.items.length / this.itemsPerPage);
    },
  },
  methods: {
    nextPage() {
      if (this.page + 1 <= this.numberOfPages) this.page += 1;
    },
    formerPage() {
      if (this.page - 1 >= 1) this.page -= 1;
    },
    updateItemsPerPage(number) {
      this.itemsPerPage = number;
    },

    filterEspecializacion() {
      console.log(this.especializacion_seleccionada);
      this.items = this.historias.filter(
        (item) => item.especializacion === this.especializacion_seleccionada
      );
    },
    filterMes(){
      this.items = this.historias.filter(
        (item) => item.fecha.substr(0,7) == this.date
      );
    },

    limpiarFiltros() {
      this.items = this.historias;
    },
  },
};
</script>
<!--items: [
        'Medicina general',
        'Odontología',
        'Ginecología',
        'Oftalmología',
        'Cirugía general',
        'Dermatología',
        'Ortopedía y traumatología',
      ],
    }),*/-->