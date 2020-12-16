<template>
  <div class="v-catalog">
    <h1>Catalog</h1>
    <router-link :to="{name: 'cart', params: { cart_data: CART } }">
      <div class="v-catalog__link-to-cart">
        Cart: {{ CART.length }}
      </div>
    </router-link>
    <div class="v-catalog__list">
      <v-catalog-item
          v-for="product in PRODUCTS"
          :key="product.article"
          :product_data="product"
          @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item";
import {mapActions, mapGetters} from 'vuex';

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
  },
  props: {},
  data() {
    return {};
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API();
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data)
    },
  },
  computed: {
    ...mapGetters([
      'PRODUCTS',
      'CART'
    ]),
  }
};
</script>

<style>
.v-catalog__list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}

.v-catalog__link-to-cart {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 16px;
  border: solid 1px #ccc;
}
</style>