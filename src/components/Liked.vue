<template>
  <div>
    <h3>Избранные товары</h3>

    <div v-show="!products.length">
      <p>У вас пока нет избранных товаров!</p>
      <router-link to="/">Перейти в каталог</router-link>
    </div>

    <div v-show="products.length">
      <ul class="product_list">
        <li v-for="product in products" :key="product.uid" class="product_item">
          <img :src="product.src" class="item_image" />
          <span class="item_name">{{ product.dish }}</span>
          <span class="item_price">{{ product.price + ' руб.' }}</span>

          <div class="product_actions">
            <button
              v-if="product.quantity === 0"
              type="button"
              class="item_button add_button"
              @click="addToCart(product)"
            >
              Добавить
            </button>
            <div v-else>
              <button
                type="button"
                class="item_button cart_button"
                @click="addToCart(product)"
              >
                +
              </button>
              <span v-if="product.quantity > 0" class="item_quantity">
                {{ product.quantity }}
              </span>
              <button
                type="button"
                class="item_button remove_button"
                @click="removeFromCart(product)"
              >
                &minus;
              </button>
            </div>

            <button
              type="button"
              class="item_button remove_like_button"
              @click="removeFromLiked(product)"
            >
              Удалить из избранного
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import { mapMutations, mapGetters } from 'vuex'

export default {
  name: 'liked',

  computed: {
    ...mapGetters({
      products: 'likedProducts',
    }),
  },
  methods: {
    ...mapMutations(['removeFromLiked', 'addToCart', 'removeFromCart']),
  },
}
</script>

<style scoped>
.product_list {
  display: flex;
  flex-wrap: wrap;
}
.product_item {
  display: flex;
  width: 300px;
  flex-direction: column;
  margin-right: 70px;
  margin-bottom: 20px;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
}
.item_image {
  margin-bottom: 10px;
}
.item_name {
  padding: 10px;
  font-weight: bold;
}
.item_price,
.item_quantity {
  padding: 10px;
}
.item_button {
  align-self: flex-start;
  padding: 4px;
  margin: 10px;
}
.product_actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.cart_button,
.remove_button {
  width: 30px;
}
.remove_like_button,
.like_button,
.add_button {
  width: 120px;
  height: 42px;
}
</style>
