<template>
  <div class="keranjang">
    <Navbar :updateKeranjang ="Keranjangs" />
    <div class="container">
      <!-- breadcrump -->
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
        <div class="col-md">
          <div class="table-responsive">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(keranjang, index) in Keranjangs" :key="keranjang.id">
                  <th scope="row">{{index+1}}</th>
                  <td>
                    <img
                      :src="'../image/'+keranjang.products.gambar"
                      class="img-fluid shadow"
                      width="250"
                    />
                  </td>
                  <td>{{keranjang.products.nama}}</td>
                  <td>{{keranjang.keterangan}}</td>
                  <td>{{keranjang.jumlah_pemesanan}}</td>
                  <td align="right">Rp. {{keranjang.products.harga}}</td>
                  <td align="right">
                    Rp.
                    <strong>{{keranjang.products.harga * keranjang.jumlah_pemesanan}}</strong>
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash @click="hapusKeranjang(keranjang.id)"></b-icon-trash>
                  </td>
                </tr>

                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga :</strong>
                  </td>
                  <td colspan="1" align="right" class="text-success">
                    <strong>Rp. {{totalHarga}}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";
export default {
  name: "Keranjang",
  components: {
    Navbar,
  },

  data() {
    return {
      Keranjangs: [],
    };
  },
    // props adalah menangkap hasil prameter yang dikirim oleh component lain ke komponen lainnya
   
  methods: {
    setKeranjang(data) {
      this.Keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/"+id)
        .then(() => {
             //    jika berhasil maka gunakan toast vue toas norification untuk notifikasinya
            this.$toast.error("sukses menghapus data", {
              // sesuaikan atribut yang di butuhkan. attributnya ada di dokumentasinya
              type: "error",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });

            // hapus data supaya tidak mereload
            axios
            .get("http://localhost:3000/keranjangs")
            .then((response)=> this.setKeranjang(response.data))
            .catch((error) =>console.log(error))
        })
        .catch((error) => console.log(error));
    },  
  },

  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjang(response.data))
      .catch((error) => console.log(error));
  },
  //   function untuk penjumlahan
  computed: {
    totalHarga() {
      return this.Keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>