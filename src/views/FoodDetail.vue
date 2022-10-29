<template>
  <div class="food-detail">
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
              <li class="breadcrumb-item active" aria-current="page">Food Order</li>
            </ol>
          </nav>
          <!-- /BreadCrumb -->
        </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <!-- <img src="" alt=""> -->
        </div>
        <div class="col-md-6">
          <h1>tes</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FoodDetail",
};
</script>
