<template>
  <div id="app" class="container mt-5">
    <img class="img-fuild m-auto d-block" src="images/cabinet.jpg" alt="Cabinet Logo">
    <router-view
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      :products="products"
      :modelPhoto="modelPhoto"
      @add="addItem"
      @delete="deleteItem"
      @setCurrentPhoto="setCurrentPhoto"
    ></router-view>
  </div>
</template>

<script>
export default {
  name: "app",
  data: function() {
    return {
      cart: [],
      products: null,
      modelPhoto:null
    };
  },
  computed: {
    cartTotal: function() {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function() {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    }
  },
  methods: {
  
    setCurrentPhoto(item){
      this.modelPhoto = item;
    },
    deleteItem: function(id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },
    addItem: function(product) {
      var whichProduct;
      var existing = this.cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });

      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    }
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>