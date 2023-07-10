<template>
    <TransitionGroup name="fade" tag="div" @beforeEnter="before" @enter="enter" @leave="leave">
        <div class="row  align-items-center" v-for="(item,index) in showItems" :key="item.id" :data-index="index">
            <div class="col-sm-6">
                <img :src="item.image" :alt="item.name" class="img-fluid d-block">
            </div>
            <div class="col-sm-6">
                <h1 class="text-info">{{ item.name }}</h1>
                <p>{{ item.description }}</p>
                <div class="h3"><price :value="Number(item.price)"></price></div>
                <button class="btn btn-info" @click="$emit('add-item', item)">+</button>
            </div>
        </div>
    </TransitionGroup>
</template>
<script>

import price from "./Price.vue";
export default {
    name:"product-data",
    components:{
        price
    },
    
    
    props:["products","maximum"],

    computed:{
        showItems:function(){
            let max = this.maximum
            return this.products.filter(function(item){
                return item.price <= Number(max)
            })
        }
    },
    methods:{
        before:function(el){
            el.className = 'd-none'
        },
        
        enter:function(el){
            var delay = el.dataset.index * 100
            setTimeout(function() {
                el.className = 'row d-flex mb-3 align-items-center animate__animated animate__fadeInRight'
            }, delay);
        },
        leave:function(el){
            var delay = el.dataset.index * 100
            setTimeout(function() {
                el.className = 'row d-flex mb-3 align-items-center'
            }, delay);
        }
    }
}
</script>