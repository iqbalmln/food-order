<template>
  <div class="home">
    <Navbar />
    <div class="container mt-4">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>Base <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link
            to="/foods"
            class="btn btn-success float-right"
          >
            <b-icon-eye /> See more
          </router-link>
        </div>
      </div>
      <div class="row mb-4 d-flex justify-content-between">
        <div class="col-md-3 mt-4" v-for="product in products" :key="product.id">
          <CardProduct
            :nama="product.nama"
            :gambar="product.gambar"
            :harga="product.harga"
            :id="product.id"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Hero from '../components/Hero.vue'
import CardProduct from '../components/CardProduct.vue'
import axios from "axios"
import Navbar from '../components/Navbar.vue'
export default {
  name: 'HomeView',
  components: {
    Hero,
    CardProduct,
    Navbar
},
  data() {
    return {
      products: []
    }
  },
  methods: {
    setProduct(data) {
      this.products = data
    }
  },
  mounted() {
    axios.get("http://localhost:3000/best-products")
      .then(response => {
        this.setProduct(response.data)
      })
      .catch(err => {
        console.log("gagal :", err);
      })
  }
}
</script>
