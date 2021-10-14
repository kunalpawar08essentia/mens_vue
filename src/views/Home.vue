<template>
  <div class="home">
    <section class="hero is-large is-dark mb-2">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to the Online Store</p>
        <p class="subtitle">The best Men's Accessories</p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <hr>
        <h2 class="is-size-5 has-text-danger has-text-centered">🅻 🅰 🆃 🅴 🆂 🆃 &nbsp  &nbsp 🅿 🆁 🅾 🅳 🆄 🅲 🆃 🆂</h2>
      </div>

      <div
        class="column is-3"
        v-for="product in latestProducts"
        v-bind:key="product.id"
        style="background-color: lightgray;"
      >
        <div class="box">
          <figure class="image is-1by1 mb-4">
            <img :src="product.get_thumbnail" />
          </figure>

          <h3 class="is-size-5">{{ product.name }}</h3>
          <p class="is-size-6 has-text-grey">₹ {{ product.price }}</p>

          <router-link
            v-bind:to="product.get_absolute_url"
            class="button is-danger is-outlined mt-4"
            >View Details</router-link
          >
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      latestProducts: [],
    };
  },
  components: {},
  mounted() {
    this.getLatestProducts();
    document.title = "Home | Accessory";
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit("setIsLoading", true);

      await axios
        .get("/api/v1/latest-products/")
        .then((response) => {
          this.latestProducts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
      this.$store.commit("setIsLoading", false);
    },
  },
};
</script>


<style scoped>

.hero {
  margin-left: -0.5rem;
  margin-right: -0.5rem;
  margin-top: -1.97rem;
  background: url("https://images.unsplash.com/photo-1441986300917-64674bd600d8?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1170&q=80");
}

</style>