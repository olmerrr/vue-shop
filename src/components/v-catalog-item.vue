<template>
  <div class='v-catalog-item'>
    <img :src="require('../assets/img/products/'+ product_data.image)" alt="img">
    <p class="v-catalog-item__name">{{product_data.name}}</p>
    <p class="v-catalog-item__price">Price: {{product_data.price}}</p>
    <button class="v-catalog-item__add-btn btn"
            @click="addToCart">Add to cart</button>
  </div>
</template>

<script>
  export default {
    name: "v-catalog-item",
    props: {
      product_data: {
        type: Object,
        default() {
          return {};
        },
      },
      cart_item_data: {
        type: Object,
        default() {
          return {};
        }
      },
    },
    data() {
      return {}
    },
    methods: {
      addToCart() {
        this.$emit('addToCart',this.product_data)
      },
    },
    computed: {}
  }
</script>

<style>
  .v-catalog-item {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: 16px;
    margin-bottom: 16px;
  }
  .v-catalog-item img {
    max-width: 150px;
    max-height: 150px;
  }
  .v-catalog-item button {
    padding:10px 14px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
</style>