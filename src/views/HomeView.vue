<template>
  <div class="home">
    <div class="container mt-4">
      <Hero />
    </div>
  </div>
</template>

<script>

import Hero from '@/components/Hero.vue'
export default {
  name: 'HomeView',
  components: {
    Hero
  }
}
</script>
