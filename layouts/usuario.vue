<template>
  <v-app>
    <!-- Menu hamburguesa -->
    <v-navigation-drawer v-model="openMenu" class="blue lighten-4" fixed app>
      <template v-slot:prepend>
        <v-list-item two-line class="d-flex justify-center">
          <v-avatar size="180">
            <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
          </v-avatar>
        </v-list-item>

        <v-list-item-content class="text-md-center">
          <v-list-item-title class="title"> Jhon Jimenez </v-list-item-title>
          <v-list-item-subtitle>Paciente</v-list-item-subtitle>
        </v-list-item-content>
      </template>

      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.id"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append>
        <div>
          <v-btn block>
            Cerrar sesión
            <v-icon> mdi-exit-to-app </v-icon>
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>

    <!--Barra de navegacion superior-->
    <v-app-bar :clipped-left="clipped" color="blue lighten-4" fixed app >
      <!--Icono que controla el menú hamburguesa -->
      <v-app-bar-nav-icon @click.stop="openMenu = !openMenu" />
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <v-spacer></v-spacer>
      <span>Codex &copy; {{ new Date().getFullYear() }}</span>
      <small>Historias clinicas</small>
      <v-spacer></v-spacer>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      openMenu: false,
      items: [
        {
          id: "perfil",
          icon: "mdi-account",
          title: "Perfil",
          to: "/Usuario/usuarioPerfil",
        },
        {
          id: "historiaClinia",
          icon: "mdi-book",
          title: "Historial Clínico",
          to: "/Usuario/usuarioHistoria",
        },
        {
          id: "examenes",
          icon: "mdi-note",
          title: "Exámenes",
          to: "/Usuario/examenes",
        },
        {
          id: "medicamentos",
          icon: "mdi-pill",
          title: "Medicamentos",
          to: "/Usuario/usuarioMedicamentos",
        },
        {
          id: "remisiones",
          icon: "mdi-text",
          title: "Remisiones",
          to: "/Usuario/usuarioRemisiones",
        },
      ],
      title: "Vuetify.js",
    };
  },
};
</script>