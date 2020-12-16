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
        :cart_item_data = "item"
        @deleteFromCart = "deleteFromCart(index)"
    >
    </v-cart-item>
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
  computed: {},
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

</style>