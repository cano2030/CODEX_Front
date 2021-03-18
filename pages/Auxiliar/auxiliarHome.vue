<template>



  <v-card>
    <v-card-title>
      <v-icon large left> </v-icon>

      <div>
        <strong class="#0c354a"
          >Búsqueda de pacientes en el banco de las EPS e IPS</strong>
      </div>
    </v-card-title>

    <v-toolbar flat color="transparent">
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Buscar Pacientes"
        single-line
      ></v-text-field>
    </v-toolbar>

    <v-list three-line
    color="#f4f9f9">
      <v-list-item
        v-for="(item, i) in searching"
        :key="i"
        ripple
        @click="() => {}"
      >
        <v-img
          :src="item.image"
          class="mr-4"
          max-width="64"
          min-width="64"
        >
        </v-img>

        <v-list-item-content>
          <span
            class="text-uppercase font-weight-regular caption"
            v-text="item.nombre"
          ></span>

          <div v-text="item.documento"></div>
          <v-btn text to="/Auxiliar/auxiliarListaExamenes"> Detalles </v-btn>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script>
export default {
  layout: "auxiliar",
  data: () => ({
    items: [
      {
        image: "https://randomuser.me/api/portraits/women/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/women/20.jpg",
        nombre: "Yesenia Lopez Giraldo",
        documento: "1365478216",
      },
      {
        image: "https://randomuser.me/api/portraits/women/30.jpg",
        nombre: "Maria Alejandra Franco Alzate",
        documento: "112365749",
      },
      {
        image: "https://randomuser.me/api/portraits/women/40.jpg",
        nombre: "Angie Rivera Hinestroza",
        documento: "114796632",
      },
      {
        image: "https://randomuser.me/api/portraits/women/50.jpg",
        nombre: "Dayana Mosquera Mosquera",
        documento: "974632114",
      },
      {
        image: "https://randomuser.me/api/portraits/women/60.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
      {
        image: "https://randomuser.me/api/portraits/men/10.jpg",
        nombre: "Mariana Palacios Hinestroza",
        documento: "123456789",
      },
    ],
    search: "",
  }),

  computed: {
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

<style>
</style>