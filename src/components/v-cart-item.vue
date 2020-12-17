<template>
  <div class="v-cart-item">
    <img class="cart__item-img"
         :src="require('../assets/img/products/'+ cart_item_data.image)" alt="img">
    <div class="v-cart-item__info">
      <p>{{ cart_item_data.name }}</p>
      <p>{{ cart_item_data.price }}</p>
      <p>{{ cart_item_data.article }}</p>
    </div>
    <div class="v-cart-item__quantity">
      <span>
        Qty: {{ cart_item_data.quantity }}
      </span>
      <button @click="deleteFromCart">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cart_item_data: {
      type: Object,
      default() {
        return {}
      }
    },
  },
  mounted() {
    this.$set(this.cart_item_data, 'quantity', 1)
  },
  methods: {
    deleteFromCart() {
      this.$emit('deleteFromCart')
    },
  },

}

</script>
<style>
  .v-cart-item {
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: 16px;
    margin-bottom: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: nowrap;
  }

  .cart__item-img {
    max-height: 100px;
    max-width: 100px;
  }
</style>