<template>
  <v-app background="../static/images/FondoIndex.png">
   
    <br />
    <center>
      <h1 style="font-family: Copperplate">APOLO SALUD</h1>
    </center>
    <br />

    <v-footer :absolute="!fixed" app>
      <v-spacer></v-spacer>
      <span> &copy; {{ new Date().getFullYear() }}</span>
      <small>| Codex</small>
      <v-spacer></v-spacer>
    </v-footer>

    <template>
      <v-row>
        <v-col cols="12" md="7"> </v-col>
        <v-col cols="12" md="4">
          <v-card class="mx-auto" style="width: 350px" elevation="12">
            <v-toolbar color="#3797a4">
              <v-card-title class="#white--text">
                <center>Iniciar sesion</center>
              </v-card-title>
              <v-spacer></v-spacer>
            </v-toolbar>

            <v-form
              ref="form"
              v-model="valid"
              class="pa-3 pt-4"
              lazy-validation
              color="#ccf2f4"
            >
              <v-spacer></v-spacer>
              <v-text-field
                v-model="usuario.user"
                :rules="rules.required"
                label="Usuario"
                style="height: 100px"
                required
              ></v-text-field>

              <v-text-field
                v-model="usuario.password"
                :rules="rules.required"
                label="Contraseña"
                style="height: 100px"
                required
              ></v-text-field>
            </v-form>
            <v-divider></v-divider>
            <v-card-actions>
              <v-btn class="white--text" color="#ee6f57" @click="validate">
                Ingresar
              </v-btn>
              <v-spacer></v-spacer>
              <v-dialog v-model="dialog" max-width="600px">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    color="#0c354a"
                    class="ma-1"
                    v-bind="attrs"
                    v-on="on"
                    plain
                  >
                    ¿Eres administrador?
                  </v-btn>
                </template>

                <v-card>
                  <v-toolbar color="#a4ebf3">
                    <v-card-title class="#0c354a--text">
                      <center>Ingresa tu codigo de administrador</center>
                    </v-card-title>
                    <v-spacer></v-spacer>
                  </v-toolbar>
                  <v-card-text>
                    <v-container>
                      <v-form ref="form" v-model="valid" lazy-validation>
                        <v-text-field
                          v-model="code"
                          :rules="rules.required"
                          label="Codigo"
                          style="height: 100px"
                          required
                        ></v-text-field>
                        <center>
                          <v-btn
                            class="white--text"
                            color="#ff5722"
                            @click="validate"
                          >
                            Ingresar
                          </v-btn>
                        </center>
                      </v-form>
                    </v-container>
                  </v-card-text>
                </v-card>
              </v-dialog>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </template>
  </v-app>
</template>

  </v-app>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    usuario: {
      user: "",
      password: "",
    },
    rules: {
      required: [(v) => !!v || "El campo es obligatorio"],
    },
  }),

  methods: {
    validate() {
      this.$refs.form.validate();
    },
  },
};
</script>
<style>
 #app { background: url("../static/images/FondoIndex.png") no-repeat center
    fixed !important; background-size: cover; }
</style>
