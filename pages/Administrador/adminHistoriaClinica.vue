  <template>
  <v-container>
    <v-card>
      <v-card-title>
        Base de datos de Pacientes
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
              <v-col cols="12" sm="6">
                <v-select
                  prepend-inner-icon="mdi-magnify"
                  solo-inverted
                  hide-details
                  :items="especializaciones"
                  label="Buscar por especialización"
                  @change="filterEspecializacion"
                ></v-select>
              </v-col>
              <v-col cols="12" sm="6">
                <v-menu
                  ref="menu"
                  v-model="menu"
                  :close-on-content-click="false"
                  :return-value.sync="date"
                  transition="scale-transition"
                  offset-y
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
                  <v-date-picker v-model="date" no-title scrollable>
                    <v-spacer></v-spacer>
                    <v-btn text color="ee6f57" @click="menu = false">
                      Cancel
                    </v-btn>
                    <v-btn text color="ee6f57" @click="$refs.menu.save(date)">
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-menu>
              </v-col>
            </v-row>
          </v-toolbar>
        </template>

        <template v-slot:default="props">
          <v-row>
            <v-col v-for="item in props.items" :key="item.name" cols="12">
              <v-card>
                <v-card-title class="subheading font-weight-bold">
                  {{ item.name }}
                </v-card-title>

                <v-divider></v-divider>

                <v-list dense>
                  <v-list-item>
                    <v-list-item-content
                      >Número de historia:</v-list-item-content
                    >
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
                    <v-list-item-content
                      >Motivo de consulta:</v-list-item-content
                    >
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

                  <v-btn class="mx-2" fab  small color="#ee6f57">
                  <v-icon color="#f4f9f9"> mdi-pencil </v-icon>
                </v-btn>
                </v-list>
              </v-card>
            </v-col>
          </v-row>
        </template>

        <template v-slot:footer>
          <v-row class="mt-2" align="center" justify="center">
            <v-spacer></v-spacer>
            <span class="mr-4 grey--text">
              Pagina {{ page }} de {{ numberOfPages }}
            </span>
            <v-btn
              fab
              dark
              color="#ee6f57"
              class="mr-1"
              @click="formerPage"
            >
              <v-icon>mdi-chevron-left</v-icon>
            </v-btn>
            <v-btn
              fab
              dark
              color="#ee6f57"
              class="ml-1"
              @click="nextPage"
            >
              <v-icon>mdi-chevron-right</v-icon>
            </v-btn>
          </v-row>
        </template>
      </v-data-iterator>
    </v-container>
  </v-container>
</template>

<script>
export default {
  layout: "admin",
  data: () => ({
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },

    page: 1,
    itemsPerPage: 3,
    filters: {},
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
    items: [
      {
        name: "Medicina general",
        num_historia: "23659",
        fecha: "2021-03-18",
        motivo_consulta: "Fiebre",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        name: "Odontología",
        num_historia: "36985",
        fecha: "2021-11-02",
        motivo_consulta: "Carie",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        name: "Dermatología",
        num_historia: "8547",
        fecha: "2021-09-10",
        motivo_consulta: "Grano",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
      {
        name: "Oftalmología",
        num_historia: "123",
        fecha: "2021-03-01",
        motivo_consulta: "Ciego",
        descripcion:
          "On the other hand, we denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, so blinded by desire, that they cannot foresee the pain and trouble that are bound to ensue; and equal blame belongs to those who fail in their duty through weakness of will, which is the same as saying through shrinking from toil and pain.",
      },
    ],

    search: "",

    headers: [
      {
        text: "Paciente",
        align: "start",
        sortable: false,
        value: "nombre",
      },
      { text: "Cedula", value: "cedula" },
      { text: "Edad", value: "edad" },
    ],
    desserts: [
      {
        nombre: "Carmensa Martinez Gomez",
        cedula: "1234567890",
        edad: "54",
      },
      {
        nombre: "Maria Camila Alzate Garnica",
        cedula: "1098765432",
        edad: "14",
      },
    ],
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    nextPage() {
      if (this.page + 1 <= this.numberOfPages) this.page += 1;
    },
    formerPage() {
      if (this.page - 1 >= 1) this.page -= 1;
    },
    updateItemsPerPage(number) {
      this.itemsPerPage = number;
    },
  },
  computed: {
    numberOfPages() {
      return Math.ceil(this.items.length / this.itemsPerPage);
    },
    searching() {
      if (!this.search) return this.items;

      const search = this.search.toLowerCase();

      return this.items.filter((item) => {
        const text = item.documento.toLowerCase();

        return text.indexOf(search) > -1;
      });
    },
  },
};
</script>
<!--filterEspecializacion(val) {
      this.filters = this.$MultiFilters.updateFilters(this.filters, {
        added_by: val,
      });
    },-->

<style>
</style>