<template>
  <nav class="menu">
    <div>
      <router-link class="router-link" to="/">Каталог</router-link>
    </div>
    <div>
      <router-link class="router-link" to="/liked"
        >Избранное ({{ itemsInLiked }})</router-link
      >
    </div>
    <div>
      <router-link class="router-link" to="/cart"
        >Корзина ({{ itemsInCart }})</router-link
      >
    </div>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'navBar',
  computed: {
    ...mapGetters(['itemsInCart', 'itemsInLiked']),
  },
}
</script>

<style scoped>
.menu {
  display: flex;
  justify-content: flex-end;
}
.menu > div {
  margin-right: 20px;
  margin-bottom: 20px;
}
.router-link {
  text-decoration: none;
}
.router-link-exact-active {
  text-decoration: underline;
}
</style>
