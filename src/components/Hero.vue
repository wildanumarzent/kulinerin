<template>
<div class="hero">
    <div class="d-none d-md-block">
    <div class="row mt-4">
        <div class="col-md">
            <div class="d-flex h-100">
               <div class="jutify-content-center align-self-center">
                    <h2><strong>Delicious Food Menu, </strong><br>In Your Gadget</h2> 
                    <p>ayo segera pilih dan pesan makanan pavorit anda</p> 
                    <router-link class="btn btn-lg btn-success" to="/foods"><b-icon-arrow-right></b-icon-arrow-right> Pesan</router-link>
                </div> 
            </div>
        </div>
        <div class="col-md">
            <img src="../assets/image/ilustrasi.png" width="100%">
        </div>
    </div>

    </div>

    <!-- mobile -->
    <div class=" d-sm-block d-md-none">
        <div class="row mt-4">
            <img src="../assets/image/ilustrasi.png" width="100%">
        <div class="col-md">
            <div class="col-md">
                <div class="d-flex h-100">
                <div class="jutify-content-center align-self-center">
                    <h2><strong>Delicious Food Menu, </strong><br>In Your Gadget</h2> 
                    <p>ayo segera pilih dan pesan makanan pavorit anda</p> 
                    <button class="btn btn-lg btn-success"><b-icon-arrow-right></b-icon-arrow-right> Pesan</button>
                </div> 
                </div>
            </div>
        </div>
    </div>

    </div>
</div>
</template>

<script>
export default {
    name:'Hero'
}
</script>

<style>

</style>