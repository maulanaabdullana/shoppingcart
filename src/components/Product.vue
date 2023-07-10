<template>
    <div>
        <h1>My Shop</h1>
        <navbar :cart="cart" :cartTotal="cartTotal" :cartQty="cartQty" @toggle-slide="toogleslider" @delete-item="deleteItem"></navbar>
        <price-slider :sliderstatus="sliderstatus" :maximum.sync="maximum"></price-slider>
        <product-data :products="products" :maximum="maximum" @add-item="addItem"></product-data>
    </div>
</template>
<script>
import ProductData from './ProductData.vue';
import PriceSlider from './priceslide.vue'
import Navbar from './navbar.vue'
export default {
    name: "products",
    props: [
        "products",
        "maximum",
        "cart",
        "cartQty",
        "cartTotal",
        "sliderstatus",
    ],
    components: {
        Navbar, ProductData, PriceSlider
    },

    methods:{
        addItem : function(item){
            this.$emit('add', item)
        },

        deleteItem: function(index){
            this.$emit('delete',index)
        },

        toogleslider:function(){
            this.$emit('toggle')
        }
    }

}
</script>