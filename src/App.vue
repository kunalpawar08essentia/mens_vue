<template>
  <div id="wrapper">
    <nav class="navbar">
      <div class="navbar-brand">
        <router-link to="/">
        <figure class="image is-64x64 ml-3 mt-3">
          <img
            class="is-rounded"
            src="https://w7.pngwing.com/pngs/419/140/png-transparent-model-computer-icons-flamenco-symbol-models-celebrities-fashion-logo.png"
          />
        </figure>
        </router-link>
        <router-link to="/" class="navbar-item has-text-danger px-4"
          ><strong>Men's Accessories</strong></router-link
        >

        <a
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbar-menu"
          @click="showMobileMenu = !showMobileMenu"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div
        class="navbar-menu"
        id="navbar-menu"
        v-bind:class="{ 'is-active': showMobileMenu }"
      >
        <div class="navbar-start">
          <div class="navbar-item">
            <form method="get" action="/search">
              <div class="field has-addons">
                <div class="control">
                  <input
                    type="text"
                    class="input is-danger is-rounded is-normal"
                    placeholder="What are you looking for?"
                    name="query"
                  />
                </div>

                <div class="control">
                  <button class="button is-danger is-rounded">
                    <span class="icon">
                      <i class="fas fa-search"></i>
                    </span>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="navbar-end">
          <router-link to="/tshirts" class="navbar-item has-text-danger">
            <strong>T-shirts</strong></router-link
          >
          <router-link to="/jeans" class="navbar-item has-text-danger">
            <strong>Jeans</strong></router-link
          >
          <router-link to="/shoes" class="navbar-item has-text-danger">
            <strong>Shoes</strong></router-link
          >
          <router-link to="/wallet" class="navbar-item has-text-danger">
            <strong>Wallet</strong></router-link
          >
          <router-link to="/belt" class="navbar-item has-text-danger">
            <strong>Belt</strong></router-link
          >

          <div class="navbar-item">
            <div class="buttons">
              <template v-if="$store.state.isAuthenticated">
                <router-link to="/my-account" class="button is-danger"
                  ><strong>My account</strong></router-link
                >
              </template>

              <template v-else>
                <router-link to="/log-in" class="button is-danger"
                  ><strong>Log in</strong></router-link
                >
              </template>

              <router-link to="/cart" class="button is-warning">
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>Cart ({{ cartTotalLength }})</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <div
      class="is-loading-bar has-text-centered"
      v-bind:class="{ 'is-loading': $store.state.isLoading }"
    >
      <div class="lds-dual-ring"></div>
    </div>

    <section class="section">
      <router-view />
    </section>

    <footer class="footer">
      <!-- <p class="has-text-centered">Copyright (c) 2021</p> -->

      <p class="has-text-centered ">Designed by Kunal Pawar</p>
    </footer>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      showMobileMenu: false,
      cart: {
        items: [],
      },
    };
  },
  beforeCreate() {
    this.$store.commit("initializeStore");

    const token = this.$store.state.token;

    if (token) {
      axios.defaults.headers.common["Authorization"] = "Token " + token;
    } else {
      axios.defaults.headers.common["Authorization"] = "";
    }
  },
  mounted() {
    this.cart = this.$store.state.cart;
  },
  computed: {
    cartTotalLength() {
      let totalLength = 0;

      for (let i = 0; i < this.cart.items.length; i++) {
        totalLength += this.cart.items[i].quantity;
      }

      return totalLength;
    },
  },
};
</script>

<style lang="scss">
@import "../node_modules/bulma";
.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #ccc;
  border-color: #ccc transparent #ccc transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.is-loading-bar {
  height: 0;
  overflow: hidden;

  -webkit-transition: all 0.3s;
  transition: all 0.3s;

  &.is-loading {
    height: 80px;

    background-color: cornsilk;
  }
}
</style>
