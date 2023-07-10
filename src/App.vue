<template>
  <div id="app" class="container mt-5">
    <router-view :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" :maximum.sync="maximum" :products="products"
      :sliderstatus="sliderstatus" @toggle="toogleslider" @add="addItem" @delete="deleteItem"></router-view>
  </div>
</template>

<script>

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderstatus: true,
    }
  },
  mounted: function () {
    fetch('https://hplussport.com/api/products/order/price')
      .then(response => response.json())
      .then(data => {
        this.products = data
      })
  },

  computed: {
    cartTotal: function () {
      let sum = 0
      for (let key in this.cart) {
        sum = sum + (this.cart[key].product.price * this.cart[key].qty)
      }
      return sum
    },
    cartQty: function () {
      let total = 0
      for (let key in this.cart) {
        total = total + this.cart[key].qty
      }
      return total
    }
  },

  methods: {
    toogleslider: function () {
      this.sliderstatus = !this.sliderstatus;
    },

    deleteItem: function (key) {
      if (this.cart[key].qty > 1) {
        this.cart[key].qty--
      } else {
        this.cart.splice(key, 1)
      }
    },

    addItem: function (product) {
      var productindex;
      var productexis = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          productindex = index
          return true
        } else {
          return false
        }
      })

      if (productexis.length) {
        this.cart[productindex].qty++
      } else {
        this.cart.push({ product: product, qty: 1 })
      }
    }
  },
}
</script>
