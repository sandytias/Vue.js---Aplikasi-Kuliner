<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2><strong>Food</strong> Lists</h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Search Your Favorite Food..."
              aria-label="Search..."
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1">
                <b-icon-search></b-icon-search>
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Foods",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFood() {
      axios
        .get("https://61bc3a72d8542f0017824619.mockapi.io/products?search=" + this.search)
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log("Gagal : ", error));
    },
  },
  mounted() {
    axios
      .get("https://61bc3a72d8542f0017824619.mockapi.io/products")
      .then((response) => 
      this.setProducts(response.data)
      // console.log(response.data)
      )
      .catch((error) => console.log("Gagal : ", error));
  },
};
</script>

<style>
</style>