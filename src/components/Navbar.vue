<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <a class="navbar-brand text-secondary" href="#">Resto</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link text-secondary" to="/"
              >Home</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link text-secondary" to="/foods"
              >Foods</router-link
            >
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link text-secondary" to="/keranjang">
              Checkout
              <b-icon-bag />
              <span class="badge badge-success ml-2">{{ updateKeranjang ? updateKeranjang : cart.length }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios';

export default {
  name: "Navbar",
  data() {
    return {
      cart: []
    }
  },
  methods: {
    cascadeCart(data) {
      this.cart = data
    }
  },
  props: [
    'updateKeranjang'
  ],
  mounted() {
    axios.get("http://localhost:3000/keranjangs")
      .then(response => {
        this.cascadeCart(response.data)
      })
      .catch(err => {
        console.log("gagal :", err);
      })
  }
};
</script>

<style scoped></style>
