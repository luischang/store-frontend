<template>
  <h6>Filtros</h6>
  <div class="category-filter">
    <q-select label="Categoría" v-model="categorySelected" :options="categories" option-value="id"
      option-label="description" @update:model-value="onChange" />
  </div>
  <div class="price-filter">

  </div>


</template>

<style></style>

<script>
export default {
  name: "ProductFilter",
  emits: ["categoriaCambiada"],
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
    onChange(value) {
      console.log("El valor seleccionado de la categoría es: " + value.id);
      this.$emit("categoriaCambiada", value.id)
    },
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
