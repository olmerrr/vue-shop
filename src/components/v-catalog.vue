<template>
  <div class="v-catalog">
    <h1>Catalog</h1>
    <router-link :to="{name: 'cart', params: { cart_data: CART } }">
      <div class="v-catalog__link-to-cart"  v-if="CART.length">
        Add to Cart: {{ CART.length }}
      </div>
    </router-link>
    <div class="filters">
      <div class="range-slider">
        <input
            type="range"
            min="0"
            max="1000" step="10"
            v-model.number="minPrice"
            @change="setChangeSlider"
        />
        <input
            type="range"
            min="0"
            max="1000"
            step="10"
            v-model.number="maxPrice"
            @change="setChangeSlider"

        />

      </div>
      <div class="range-values">
        <p>Min: {{minPrice}}</p>
        <p>Max: {{maxPrice}}</p>
      </div>
    </div>

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
  data() {
    return {
      minPrice: 0,
      maxPrice: 1000,
    };
  },
  props: {},
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
    setChangeSlider() {
      if (this.minPrice > this.maxPrice) {
        let temp = this.maxPrice;
        this.maxPrice = this.minPrice;
        this.minPrice = temp;
      }


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

<style scoped>
  .v-catalog__list {
     display: flex;
     flex-wrap: wrap;
     justify-content: space-between;
     align-items: center;
   }
  .v-catalog__link-to-cart {
     position: fixed;
     top: 10px;
     right: 10px;
     padding: $padding*2;
     border: solid 1px #aeaeae ;
     background: #ffffff;
   }
  .filters {
    padding: 20px 0;
    display: flex;
    justify-content: space-between;
  }
  .range-slider input[type=range] {
    position: absolute;
    left: 65%;
    top: 180px;
  }
  ::-webkit-slider-thumb {
    z-index: 2;
    position: relative;
    top: 2px;
    margin-top: -7px;
  }
  input[type=range]{
    -webkit-appearance: none;
  }
  input[type=range]::-webkit-slider-runnable-track {
    width: 300px;
    height: 5px;
    background: #ddd;
    border: none;
    border-radius: 3px;
  }
  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    border: 1.5px solid #C1C1C1;
    height: 16px;
    width: 16px;
    border-radius: 50%;
    background: #EDEDED;
  }
  input[type=range]:focus {
    outline: none;
  }
  input[type=range]::-webkit-slider-runnable-track {
    width: 100%;
    height: 5px;
    box-shadow: 1px 1px 1px #C6C6C6, 0px 0px 1px #787878;
    border-radius: 2px;
    border: 0.2px solid #787878;
}
</style>