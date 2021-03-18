<template>
  <div>
    <div class="d-flex justify-space-between mb-6">
      <h1>Historia Clínica</h1>
      <v-btn class="mx-2" fab dark small color="cyan">
        <v-icon dark> mdi-share </v-icon>
      </v-btn>
    </div>
     <v-select
      v-model="select"
      :items="items"
      label="Buscar especialidad"  
    ></v-select>
  </div>
</template>

<script>
export default {
  layout: "usuario",
 data: () => ({
      items: [
        'Medicina general',
        'Odontología',
        'Ginecología',
        'Oftalmología',
        'Cirugía general',
        'Dermatología',
        'Ortopedía y traumatología',
      ],
    }),
};
</script>