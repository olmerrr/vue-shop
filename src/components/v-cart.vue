<template>
  <div class='v-cart'>
    <h2>Cart</h2>
    <router-link :to="{name: 'catalog' }">
      <div class="v-catalog__link-to-cart">
        Back to catalog:
      </div>
    </router-link>
    <p v-if="!cart_data.length">In your Cart nothing.. Please add some product in your cart</p>
    <v-cart-item
        v-for="(item, index) in cart_data"
        :key="item.article"
        :cart_item_data="item"
        @deleteFromCart="deleteFromCart(index)"
    >
    </v-cart-item>
    <div class="v-cart__total">
      <p class="total__name">Total: </p>
      <p>{{cartTotalCost}} $</p>
    </div>
  </div>
</template>

<script>
import vCartItem from './v-cart-item';
import {mapActions} from 'vuex';

export default {
  name: "v-cart",
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {}
  },
  components: {
    vCartItem,
  },
  computed: {
    cartTotalCost() {
      let result  = [];

      if (this.cart_data.length){
          for (let item of this.cart_data) {
            result.push(item.price * item.quantity);
          }
          result = result.reduce((sum, el) => {
            return sum + el;
          })
        return result;
      } else {
        return 0;
      }
    },
  },
  methods: {
    ...mapActions([
      'DELETE_FROM_CART'
    ]),
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
}
</script>

<style scoped>
  .v-cart__total {
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    padding: 20px;
    display: flex;
    justify-content: center;
    font-size: 18px;
    font-weight: 500;
    background-color: #3f9465;
    color: #ffffff;
  }

  .total__name {
    margin-right: 20px;
  }
</style>