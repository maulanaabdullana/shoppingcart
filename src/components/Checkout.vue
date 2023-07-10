<template>
    <div>
        <table class="table table-hover">
            <caption class="text-right">
                <b>Total</b>
                <price :value="Number(cartTotal)"></price>
            </caption>
            <thead>
                <tr>
                    <th scope="col">Item</th>
                    <th scope="col">Qty</th>
                    <th scope="col">Price</th>
                    <th scope="col">Subtotal</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item,index) in cart" :key="item.product.id">
                    <th scope="row">{{ item.product.name }}</th>
                    <th>{{ item.qty }}</th>
                    <th>{{ item.product.price }}</th>
                    <th>{{ item.product.price * item.qty }}</th>
                    <th>
                        <button class="btn btn-info" @click="$emit('add',item.product)">+</button>
                        <button class="btn btn-danger" @click="$emit('delete',index)">-</button>
                    </th>
                </tr>
            </tbody>
        </table>
        <router-link class="btn btn-sm btn-outline-info text-dark" to="/">Kembali Ke dashboard</router-link>

    </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import Price from './Price.vue'
export default {
    name: "checkout",
    props: ["cart", "cartTotal"],
    components: {
        Price,
        FontAwesomeIcon
    }
}
</script>