<template>
  <v-card
    class="overflow-hidden"
  >
    <v-toolbar
      flat
      
    >
      <v-icon color="#0c354a">mdi-account</v-icon>
      <v-toolbar-title class="#0c354a">
        Perfil de usuario
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        class="white--text"
        color="#ff5722"
        fab
        small
        @click="isEditing = !isEditing"
      >
        <v-icon v-if="isEditing">
          mdi-close
        </v-icon>
        <v-icon v-else >
          mdi-pencil
        </v-icon>
      </v-btn>
    </v-toolbar>
    <v-card-text>
      <v-text-field
        :disabled="!isEditing"
        color="white"
        label="Name"
      ></v-text-field>
      <v-text-field
        :disabled="!isEditing"
        color="white"
        label="Apellido"
      ></v-text-field>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
      class="white--text"
        
        :disabled="!isEditing"
        color="#ff5722"
        @click="save"
      >
        Save
      </v-btn>
      
    </v-card-actions>
    <v-snackbar
      v-model="hasSaved"
      :timeout="2000"
      absolute
      bottom
      left
    >
      Tu perfil ha sido actualizado con exito
    </v-snackbar>
  </v-card>
</template>


<script>
  export default {
      layout: "auxiliar",
    data () {
      return {
        hasSaved: false,
        isEditing: null,
        model: null,
      }
    },

    methods: {
      customFilter (item, queryText, itemText) {
        const textOne = item.name.toLowerCase()
        const searchText = queryText.toLowerCase()

        return textOne.indexOf(searchText) > -1 ||
          textTwo.indexOf(searchText) > -1
      },
      save () {
        this.isEditing = !this.isEditing
        this.hasSaved = true
      },
    },
  }
</script>
<style>

</style>