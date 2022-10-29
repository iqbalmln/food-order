<template>
  <div class="hero">
    <!-- Desktop -->
    <div class="d-none d-md-block">
      <div class="row">
        <div class="col-md-6 d-flex align-items-center">
          <div>
            <h2><strong>Delicious Food Menu,</strong><br />in Your Gadget</h2>
            <p>Ayo segera pilih dan pesan makanan favorit anda</p>
            <router-link class="btn btn-success" to="/foods">
              <b-icon-arrow-right></b-icon-arrow-right> Pesan
            </router-link>
          </div>
        </div>
        <div class="col-md-6">
          <img src="@/assets/img/hero.png" width="100%" alt="" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-block d-md-none">
      <div class="row">
        <div class="col-md-6 mb-3">
          <img src="../assets/img/hero.png" width="100%" alt="" />
        </div>
        <div class="col-md-6 d-flex align-items-center">
          <div class="text-center">
            <h2><strong>Delicious Food Menu,</strong>in Your Gadget</h2>
            <p>Ayo segera pilih dan pesan makanan favorit anda</p>
            <router-link class="btn btn-success" to="/foods">
              <b-icon-arrow-right></b-icon-arrow-right> Pesan
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>
