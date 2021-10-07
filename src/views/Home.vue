<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to the Online Store</p>
        <p class="subtitle">The best Men's Accessories</p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>

      <div
        class="column is-3"
        v-for="product in latestProducts"
        v-bind:key="product.id"
        style="background-color: lightgray;"
      >
        <div class="box">
          <figure class="image mb-4">
            <img :src="product.get_thumbnail" />
          </figure>

          <h3 class="is-size-4">{{ product.name }}</h3>
          <p class="is-size-6 has-text-grey">₹{{ product.price }}</p>

          <router-link
            v-bind:to="product.get_absolute_url"
            class="button is-dark mt-4"
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
  /* margin-left: -2.97rem;
  margin-right: -2.97rem; */
  margin-top: -1.5rem;
  background: url("https://images.unsplash.com/photo-1633574364467-808a45292353?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1171&q=80");
}
</style>