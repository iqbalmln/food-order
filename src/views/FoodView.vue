<template>
  <div class="container">
    <div class="row mt-4">
      <div class="col">
        <h2>Daftar <strong>Makanan</strong></h2>
      </div>
    </div>
    <div class="row mt-3">
      <div class="col">
        <div class="input-group flex-nowrap">
          <input
            v-model="search"
            type="text"
            class="form-control"
            placeholder="Cari Makanan Kesukaan Anda"
            aria-label="Cari"
            aria-describedby="addon-wrapping"
            @keyup="searchFood()"
          />
          <span class="input-group-text" id="addon-wrapping"
            ><b-icon-search></b-icon-search
          ></span>
        </div>
      </div>
    </div>
    <div class="row mb-4">
      <div class="mt-4 col-md-4" v-for="product in products" :key="product.id">
        <CardProduct
          class="border"
          :nama="product.nama"
          :gambar="product.gambar"
          :harga="product.harga"
          :id="product.id"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardProduct from "../components/CardProduct.vue";
export default {
  name: "Food",
  components: {
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFood() {
      axios.get("http://localhost:3000/products?q=" + this.search)
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
