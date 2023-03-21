<template>
  <header>
    <the-header
      :cartList="cartList"
      @handle-delete-cart="handleDelete"
      @handle-amount-cart="handleAmount"
    />
  </header>
  <main class="container">
    <product-list @handle-buy="handleBuy" />
  </main>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  components: {
    TheHeader,
    ProductList,
  },
  data() {
    return {
      cartList: [],
    };
  },
  methods: {
    handleBuy(productItem) {
      const index = this.cartList.findIndex(
        (cart) => cart.id === productItem.id
      );
      if (index !== -1) {
        this.cartList[index].amount += 1;
      } else {
        const newProductItem = { ...productItem, amount: 1 };
        this.cartList = [...this.cartList, newProductItem];
        // this.cartList.push(productItem);
      }
    },
    handleDelete(cart) {
      this.cartList = this.cartList.filter((product) => product.id !== cart.id);
    },
    handleAmount(cart, flag) {
      let index = this.cartList.findIndex(
        (product) => product.id === cart.id
      );
      if (flag) {
        if (this.cartList[index].amount < this.cartList[index].quantityInStock) {
          this.cartList[index].amount += 1;     
        } else {
          alert("Số lượng bạn mua không thể lớn hơn số hàng trong kho!");
        }
      } else {
        if (this.cartList[index].amount === 1) {
          alert("Không thể giảm số lượng dưới 1!");
        } else {
          this.cartList[index].amount -= 1;
        }
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
