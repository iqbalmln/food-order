<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs.length" />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><a href="/">Home</a></li>
              <li class="breadcrumb-item"><a href="/foods">Library</a></li>
              <li class="breadcrumb-item active" aria-current="page">Data</li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Photo</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../asset/img/' + keranjang.product.gambar"
                      alt=""
                      width="250"
                    />
                  </td>
                  <td>{{ keranjang.product.nama }}</td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td align="center">{{ keranjang.jumlah_pemesanan }}</td>
                  <td align="right">Rp. {{ keranjang.product.harga }}</td>
                  <td align="right">
                    <strong>
                      Rp.
                      {{ keranjang.product.harga * keranjang.jumlah_pemesanan }}
                    </strong>
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      style="cursor: pointer"
                      @click="deleteKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">Total Harga :</td>
                  <td colspan="6" align="right">{{ totalHarga }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <!-- Form checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form @submit.prevent>
            <div class="form-group">
              <label for="nama">Nama :</label>
              <input type="text" class="form-control" v-model="pesan.nama" />
            </div>
            <div class="form-group">
              <label fo="noMeja">No Meja :</label>
              <textarea
                class="form-control"
                placeholder="noMeja spt : Pedas, Nasi setengah .."
                v-model="pesan.noMeja"
              ></textarea>
            </div>
            <button
              type="submit"
              class="btn btn-success float-right"
              @click="checkout()"
            >
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
  name: "Keranjang",
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data;
    },
    deleteKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Pesanan dihapus!", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
          // Reload page for user cart update
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => {
              this.setKeranjang(response.data);
            })
            .catch((err) => {
              console.log("gagal :", err);
            });
        })
        .catch((err) => {
          console.log("gagal :", err);
        });
    },
    checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.kerajangs = this.keranjangs;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus keranjang
            this.keranjangs.map((item) => {
              return axios
                .delete("http://localhost:3000/keranjangs/" + item.id)
                .catch((error) => console.log(error));
            });
            // redirect pesanan sukses page
            this.$router.push({ path: "/pesanan-sukses" });

            // pop-up notification
            this.$toast.success("Berhasil Memesan!", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch(() => {
            this.$toast.error("Gagal Memesan!", {
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          });
      } else {
        this.$toast.error("Nama dan nomor meja harus diisi!", {
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
      .get("http://localhost:3000/keranjangs")
      .then((response) => {
        this.setKeranjang(response.data);
      })
      .catch((err) => {
        console.log("gagal :", err);
      });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items + data.product.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
  components: { Navbar },
};
</script>

<style lang="scss" scoped></style>
