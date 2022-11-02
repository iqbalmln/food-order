<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <!-- BreadCrumb -->
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
          <!-- /BreadCrumb -->
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <div>
            <img
              style="width: 100%; height: 100%; object-fit: cover"
              :src="`../asset/img/${product.gambar}`"
            />
          </div>
        </div>
        <div class="col-md-6">
          <h2 class="">
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <p>{{ product.kode }}</p>
          <h4>
            Harga: <strong>{{ product.harga }}</strong>
          </h4>
          <form @submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pesan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label>Keterangam</label>
              <textarea
                class="form-control"
                placeholder="Keterangan spt : Pedas, Nasi setengah .."
                v-model="pesan.keterangan"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan()">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Navbar from "../components/Navbar.vue";

export default {
    name: "FoodDetail",
    data() {
        return {
            product: {},
            pesan: {},
        };
    },
    methods: {
        setProduct(data) {
            this.product = data;
        },
        pemesanan() {
            if (this.pesan.jumlah_pemesanan) {
                this.pesan.product = this.product;
                axios
                    .post("http://localhost:3000/keranjangs", this.pesan)
                    .then(() => this.$router.push({ path: "/keranjang" }), this.$toast.success("Sukses Masuk Keranjang!", {
                    type: "success",
                    position: "top-right",
                    duration: 3000,
                    dismissible: true,
                }))
                    .catch((err) => console.log(err));
            }
            else {
                this.$toast.error("Jumlah pemesanan harus diisi!", {
                    type: "error",
                    position: "top-right",
                    duration: 3000,
                    dismissible: true,
                });
            }
        },
    },
    mounted() {
        axios
            .get("http://localhost:3000/products/" + this.$route.params.id)
            // .then(response => console.log(response.data))
            .then((response) => this.setProduct(response.data))
            .catch((error) => console.log(error));
    },
    components: { Navbar }
};
</script>
