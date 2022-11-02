<template>
  <div class="card shadow" style="width: 18rem">
    <img :src="`../asset/img/${gambar}`" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ nama }}</h5>
      <p class="card-text">Harga : Rp. {{ harga }}</p>
      <router-link
        :to="'/foods/' + id"
        class="btn btn-success"
      >
        <b-icon-cart></b-icon-cart> Pesan</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["nama", "harga", "gambar", "id"],
};
</script>
