<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col-md">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods">foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Foods Order</li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <img :src="'../image/'+product.gambar" class="img-fluid shadow card-img-top" alt="..." />
        </div>

        <div class="col-md-6">
          <h2>
            <strong>{{product.nama}}</strong>
          </h2>
          <hr />
          <h4>
            harga
            <strong>Rp : {{product.harga}}</strong>
          </h4>

          <form action v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pesanan">Jumalah pesanan</label>
              <input type="text" class="form-control" v-model="pesan.jumlah_pemesanan" />
            </div>

            <div class="form-group">
              <label for="keterangan">keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                name
                placeholder="masukan keterangan sperti : nasi setengah.."
                class="form-control"
              ></textarea>
            </div>

            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },

  methods: {
    SetProduct(data) {
      this.product = data;
    },
    pemesanan() {
      // isi keranjang dengan sesuai pesanan
      if (this.pesan.jumlah_pemesanan) {
         // isi dengan product dan memanggil product kedalam pesan
      this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            //   melempar data detail pesanan ke view keranjang
            this.$router.push({path :"/keranjang"});
            //    jika berhasil maka gunakan toast vue toas norification untuk notifikasinya
            this.$toast.success("sukses masuk keranjang", {
              // sesuaikan atribut yang di butuhkan. attributnya ada di dokumentasinya
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      }else{
           this.$toast.error("Jumlah pesanan harus di isi", {
              // sesuaikan atribut yang di butuhkan. attributnya ada di dokumentasinya
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissible: false,
            });
      }
    },
  },

  mounted() {
    axios
      // mengambil data dari backend
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) =>
        // handle success
        // mengambil response dari data object
        this.SetProduct(response.data)
      )
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>