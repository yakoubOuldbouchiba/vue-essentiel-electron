<template>
  <div>
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal"></navbar>
    <h1 class="text-center mt-0">Shop</h1>
    <p>You're clever to choose us</p>
    <product-list 
      :products="products"
      :modelPhoto="modelPhoto"
    >
    </product-list>
  </div>
</template>
<script>
import Navbar from "./Navbar.vue";
import ProductList from "./ProductList.vue";

export default {
  name: "products",
  props: [
    "products",
    "cart",
    "cartQty",
    "cartTotal",
    "modelPhoto"
  ],
  components: {
    Navbar,
    ProductList
  }
};
</script>
