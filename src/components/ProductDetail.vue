<template>
  <section class="container">
    <div class="row">
        <div class="col-4">
            <img class="img-thumbnail" :src="product.image" alt="productItem.image">
        </div>
        <div class="col-8 text-justify">
            <div class="alert alert-success">
                <b>Name: </b>
                <span>{{product.name}}</span>
            </div>
            <div class="alert alert-success">
                <b>Mô tả: </b>
                <span>{{product.description}}</span>
            </div>
            <div class="alert alert-success">
                <b>Giá bán: </b>
                <span>{{product.price.toLocaleString()}} VND</span>
            </div>
            <div class="alert alert-success">
                <b>Số lượng tồn kho: </b>
                <span>{{product.quantityInStock}}</span>
            </div>
        </div>
      </div>
  </section>
</template>

<script>
export default {
    props:{
        product:{
            type: Object
        }
    }
}
</script>

<style>

</style>