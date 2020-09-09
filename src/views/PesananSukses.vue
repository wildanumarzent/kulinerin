<template>
  <div class="pesan">
      <Navbar />
      <div class="container">
          <div class="row justify-content-center mt-5">
              <div class="col text-center">
                  <img src="../assets/image/menunggu.png" width="300" alt="">
                   <h2><strong>Suksess !!</strong></h2>
                  <h4>Selamat Pesanan Anda Sedang Di Proses <br>Selamat Menunggu </h4>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';

export default {
    name: 'PesananSukses',
    components: {
        Navbar
    }
}
</script>

<style>

</style>