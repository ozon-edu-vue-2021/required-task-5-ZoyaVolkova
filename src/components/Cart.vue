<template>
  <div>
    <h3>Корзина</h3>
    <div v-show="!products.length">
      <p>Ваша корзина пуста!</p>
      <router-link to="/">Продолжить покупки</router-link>
    </div>

    <div v-show="products.length">
      <div class="cart_list">
        <div v-for="p in products" :key="p.uid">
          <div class="cart_item">
            <span>{{ p.dish }}</span>
            <span>Количество: {{ p.quantity }}</span>
            <span> {{ p.price * p.quantity }} руб.</span>
            <div>
              <button
                type="button"
                class="item_button cart_button"
                @click="addToCart(p)"
              >
                +
              </button>
              <button
                type="button"
                class="item_button remove_button"
                @click="removeFromCart(p)"
              >
                Удалить
              </button>
            </div>
          </div>
        </div>
      </div>
      <span class="total">Общая сумма: {{ total }} руб.</span>
    </div>

    <button v-show="products.length" @click="checkout" class="checkout">
      Оформить
    </button>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'

export default {
  computed: {
    ...mapGetters({
      products: 'cartProducts',
      total: 'total',
    }),
  },
  methods: {
    ...mapMutations(['addToCart', 'removeFromCart']),
    checkout() {
      const string = this.products
        .map((item) => {
          return item.dish + ' ' + item.quantity + ' шт.'
        })
        .join('\n')

      alert(string + '\nОбщая стоимость ' + this.total + ' руб.')
    },
  },
}
</script>

<style scoped>
.cart_list {
  margin-bottom: 20px;
}
.cart_item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 50px;
  border-bottom: 1px solid gray;
}
.cart_item > span {
  width: 300px;
}
.item_button {
  margin-right: 10px;
}
.cart_button {
  width: 30px;
}
.checkout {
  padding: 5px;
  margin-top: 10px;
}
.total {
  font-weight: bold;
}
</style>
