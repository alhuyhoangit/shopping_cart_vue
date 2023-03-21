<template>
  <table class="table">
    <thead>
      <tr>
        <th>STT</th>
        <th>Tên</th>
        <th>Giá</th>
        <th>Số lượng trong kho</th>
        <th>Số lượng</th>
        <th>Thành tiền</th>
        <th>Hành động</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(cart, index) in cartList" :key="index">
        <td>{{ index + 1 }}</td>
        <td>{{ cart.name }}</td>
        <td>{{ cart.price.toLocaleString() }}</td>
        <td>{{ cart.quantityInStock.toLocaleString() }}</td>
        <td>   
          <button class="btn btn-success" @click="handleAmount(cart,false)">
            <i class="fa fa-arrow-down"></i>
          </button>
          <span class="mx-2">{{ cart.amount }}</span>
          <button class="btn btn-success" @click="handleAmount(cart,true)">
            <i class="fa fa-arrow-up"></i>
          </button>
        </td>
        <td>{{ (cart.price * cart.amount).toLocaleString() }}</td>
        <td>
          <button @click="handleDelete(cart)" class="btn btn-danger">
            <i class="fa fa-trash"></i>
          </button>
        </td>
      </tr>
      <tr>
        <td>Tổng tiền:</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td class="text-danger font-weight-bold">
          {{ sumMoney.toLocaleString() }}
        </td>
        <td></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    cartList: {
      type: Array,
    },
  },
  computed: {
    sumMoney() {
      return this.cartList.reduce(
        (sum, product) => (sum += product.price * product.amount),
        0
      );
    },
  },
  methods: {
    handleDelete(cart) {
      this.$emit("handle-delete-cart", cart);
    },
    handleAmount(cart,flag){
      this.$emit("handle-amount-cart",cart, flag);
    }
  },
};
</script>

<style></style>
