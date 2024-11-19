<template>
  <h5>Listado de Productos</h5>
  <div class="product-list">
    <div class="product-grid">
      <div class="product-item" v-for="item in products" :key="item.id">
        <ProductItem :product="item" />
      </div>
    </div>
  </div>
</template>

<style>
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
}
</style>

<script>
import ProductItem from "src/components/product/ProductItem.vue"

export default {
  name: "ProductList",
  components: { ProductItem },
  data() {
    return {
      products: []
    }
  },
  mounted() {
    this.cargarProductos();
  },
  methods: {
    cargarProductos() {
      let endpointURL = "/api/product";
      let token = JSON.parse(localStorage.getItem("userData")).token;
      let headers = {
        headers: {
          "Authorization": "Bearer " + token,
          "Content-Type": "application/json"
        }
      }
      this.$api.get(endpointURL, headers)
        .then(response => {
          this.products = response.data;
        }).catch(error => {
          console.log(error);
          this.$q.notify({ message: 'Ocurrió un error', color: 'negative' });
          this.$router.push("/")
        });
    }
  }
}


</script>
