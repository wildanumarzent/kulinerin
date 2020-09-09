<template>
    <div>
        <Navbar />
        <div class="container">
            <div class="row">
                <div class="col-md">
                    <h2>Daftar <strong>Makanan</strong></h2>
                </div>
            </div>
            <div class="row mt-3">
                <div class="col-md">
                    <div class="input-group mb-3">
                        <input v-model="search" type="text" class="form-control" placeholder="Cari makanan kesukaan anda.." aria-label="cari" aria-describedby="basic-addon1" @keyup="setSeacrhFood">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="basic-addon1"> <b-icon-search></b-icon-search> </span>
                        </div>
                        </div>
                    </div>
            </div>

            <div class="row mb-4">
                <div class="col-md-3 mt-4" v-for="product in products" :key="product.id" >
                    <CardProduct :product= "product" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'
export default {
    name:'Foods',
    components: {
        Navbar,
        CardProduct
    },
    data(){
        return {
            products : [],
            search: ''
        };
    },
    methods: {
        setProduct(data) {
            this.products = data
        },
        setSeacrhFood() {
        axios 
        .get('http://localhost:3000/products?q='+this.search)
        .then((response)=>this.setProduct(response.data))
        .catch((error) => console.log(error))
        }
    },

    mounted(){
        axios 
        .get('http://localhost:3000/products')
        .then((response)=>this.setProduct(response.data))
        .catch((error) => console.log(error))
    },
};
</script>

<style>

</style>