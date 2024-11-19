<template>
  <h6>Filtros</h6>
  <div class="category-filter">
    <q-select label="Categoría" v-model="categorySelected" :options="categories" option-value="id"
      option-label="description" />
  </div>
  <div class="price-filter">

  </div>


</template>

<style></style>

<script>
export default {
  name: "ProductFilter",
  data() {
    return {
      minimo: 0,
      maximo: 0,
      categories: [],
      categorySelected: null
    }
  },
  mounted() {
    this.cargarCategorias();
  },
  methods: {
    cargarCategorias() {
      let endpointURL = "/api/category";
      this.$api.get(endpointURL)
        .then(response => {
          this.categories = response.data;
        })
        .catch(error => {
          console.error(error);
        });

    }
  }
}

</script>
