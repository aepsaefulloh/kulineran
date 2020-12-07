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
          <form action="" class="mt-4">
            <div class="form-group">
              <label for="jumlah-pemesanan">Jumlah Pesanan</label>
              <input type="number" class="form-control" />
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Keterangan spt : pedes, nasi setengah, ga pake kecap, dll."
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success">
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
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
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