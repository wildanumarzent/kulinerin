<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />

      <div class="row mt-4">
        <div class="col">
          <h2>Best<strong>Product</strong>
          </h2>
        </div>
        <div class="col">
          <router-link to="foods" class="btn btn-success">
            <b-icon-eye></b-icon-eye>Lihat semua
          </router-link>
        </div>
      </div>
                            <!-- melempat data dari response setproduct(response.data) lalu di looping -->
      <div class="row mb-4">
        <div class="col-md-3 mt-4" v-for="product in products" :key="product.id">
        <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },
  // inisialisasi product dengan array kosong terlebih dahulu,  ntar isi dengan setProduct di methods
  data() {
    return {
      products: []
    }
  },
  // method untuk mengisi nilai product yang kosong
  methods: {
    setProduct(data) {
      this.products = data;
    },
  },
  // baru jalankan data productnya dengan axios.
  mounted() {
    axios
    // mengambil data dari backend
      .get("http://localhost:3000/best-products")
      .then((response)=>
      // handle success
      // mengambil response dari data object 
      this.setProduct(response.data))
      .catch((error)=>console.log(error))
  },
};
</script>
