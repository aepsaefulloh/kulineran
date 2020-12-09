<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col mt-5">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/img/foods/' + product.gambar"
            class="img-fluid shadow img-detail"
            alt=""
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga : <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form action="" class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah-pemesanan">Jumlah Pesanan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea
                class="form-control"
                v-model="pesan.keterangan"
                placeholder="Keterangan spt : pedes, nasi setengah, ga pake kecap, dll."
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart> Pesan
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
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
     if(this.pesan.jumlah_pemesanan){
        this.pesan.products = this.product;
      axios
        .post("http://localhost:3000/keranjangs", this.pesan)
        .then(() => {
          this.$router.push({path: "/keranjang"})
          this.$toast.success("Pemesanan Sukses", {
            type:'success',
            position: 'top-right',
            duration: 3000,
            dismissible:true
          });
        })
        .catch((err) => {
          console.log(err);
        });
     }else{
 this.pesan.products = this.product;
      axios
        .post("http://localhost:3000/keranjangs", this.pesan)
        .then(() => {
          this.$toast.success("Jumlah Pesanan Harus Diisi", {
            type:'error',
            position: 'top-right',
            duration: 3000,
            dismissible:true
          });
        })
        .catch((err) => {
          console.log(err);
        });
     }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style lang="scss" scoped>
</style>