<template>
  <v-card color="#3797a4">
    <v-card-title class="#0c354a--text">
      Examenes
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        color="#0c354a"
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
                <v-toolbar color="#3797a4">
                  <v-card-title>
                    <span class="headline">Añadir nuevo examen</span>
                  </v-card-title>
                </v-toolbar>
                <v-card-text>
                  <v-form ref="formExamen" v-model="valid" lazy-validation>
                    <v-container>
                      <v-row>
                        <v-col cols="12" sm="8" md="6">
                          <v-text-field
                            label="Numero de Identificación (Paciente)"
                            required
                            :disabled="true"
                            v-model="paciente.cedula"
                            
                          
                            :rules="rules.required"
                            
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="8" md="6">
                          <v-text-field
                            label="Numero de Identificación (Medico/Auxiliar)"
                            required
                            :disabled="true"
                            
                            v-model="auxiliar.cedula"
                            :rules="rules.required"
                          ></v-text-field>
                        </v-col>

                        <v-col cols="12">
                          <v-select
                            :items="area"
                            label="Area de laboratorio"
                            :rules="rules.required"
                            v-model="examen.arealab"
                            required
                          ></v-select>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            label="Nombre del examen"
                            required
                            :rules="rules.required"
                            v-model="examen.nombre"
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
                  </v-form>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="dialog = false">
                    Cerrar
                  </v-btn>
                  <v-btn color="blue darken-1" text @click="GuardarExamen()">
                    Guardar
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
import auxiliarPerfilVue from './auxiliarPerfil.vue';
const url_apiexamen = "http://localhost:3001/examenes/";

export default {
  beforeMount() {
    this.loadUser();
    //this.getPacientes();
  },
  //this.$router.push("Medico/MedicoHome");
  layout: "auxiliar",

  data() {
    return {
      auxiliar:{},
      paciente:{},
      rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
      dialog: false,
      search: "",
      area:['Hematología y coagulación','Químicas','Orina y heces','Inmunología','Serología','	Microbiología','Citometría de flujo y biología molecular'],
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
       examen:{
        idpaciente:'',
        idauxiliar:'',
        arealab:'',
        nombre:'',
        fecha:new Date().getDay()+"/"+new Date().getMonth()+"/"+new Date().getFullYear()
      },
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
  methods: {
    
    loadUser() {
      let stringUser=localStorage.getItem("user-system");
      this.auxiliar = JSON.parse(stringUser);
      let stringUser2=localStorage.getItem("user-detalle");
      this.paciente = JSON.parse(stringUser2);
    },

    validate() {
      this.$refs.form.validate();
    },

    async GuardarExamen() {
      this.examen.idpaciente=this.paciente.cedula;
      this.examen.idauxiliar=this.auxiliar.cedula;
      
      if (this.$refs.formExamen.validate()) {
        // Crear un nuevo objeto con la info del usuario
        try {
          let examen = Object.assign({}, this.examen);
          let response = await this.$axios.post(url_apiexamen, examen);
          this.$swal.fire({
            type: "success",
            title: "Operación exitosa.",
            text: "El examen se guardó correctamente.",
          });
        } catch (error) {
          console.log(error);
        }
        this.dialog = false;
      } else {
        this.$swal.fire({
          type: "warning",
          title: "Formulario incompleto.",
          text: "Hay campos que deben ser diligenciados.",
        });
      }
      
    },
  },
};
</script>

<style>
</style>