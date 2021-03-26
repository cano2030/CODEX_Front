<template>
  <v-app>
    <!-- Menu hamburguesa -->
    <v-navigation-drawer v-model="openMenu" color="#a4ebf3" fixed app>
      <template v-slot:prepend>
        <v-list-item two-line>
          <v-avatar size="180">
            <v-img
              src="https://res.cloudinary.com/postedin/image/upload/d_psu:no-image.jpg,f_auto,q_80/psu/c-postedin-image-65344.jpeg"
             
            ></v-img>
          </v-avatar>
        </v-list-item>

        <v-list-item-content>
          <v-list-item-title class="text-md-center">
            Karen Johana Mosquera
          </v-list-item-title>
          <v-list-item-subtitle class="text-md-center"
            >Auxiliar de Enfermeria</v-list-item-subtitle
          >
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
          <v-btn block text to="/">
            Logout
            <v-icon> mdi-exit-to-app </v-icon>
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>

    <!--Barra de navegacion superior-->
    <v-app-bar :clipped-left="clipped" fixed app color="#ccf2f4">
      <!--Icono que controla el menú hamburguesa -->
      <v-app-bar-nav-icon @click.stop="openMenu = !openMenu" />

      <v-toolbar-items>
        <img
          src="../static/images/logoapolo.PNG"
          max-width="64"
          min-width="64"
        />
      </v-toolbar-items>
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
          id: "homeauxiliar",
          icon: "mdi-home",
          title: "Home",
          to: "/Medico/MedicoHome",
        },
        {
          id: "perfilauxiliar",
          icon: "mdi-account",
          title: "Perfil",
          to: "/Medico/MedicoPerfil",
        },
      ],
      title: "Vuetify.js",
    };
  },
};
</script>