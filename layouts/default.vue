<template>
  <div class="h-full w-full">
    <Navbar />
    <div class="container mx-auto">
      <div class="px-6 sm:px-12 pt-36 pb-12">
        <Nuxt />
      </div>
    </div>
    <Footer />
  </div>
</template>
<script>
import Navbar from '../components/Navbar'
import Footer from '../components/Footer'
export default {
  components: { Footer, Navbar },
}
</script>
