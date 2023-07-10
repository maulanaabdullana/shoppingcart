<template>
    <transition name="fade" enter-active-class=" animate__animated animate__fadeInRight">
        <div v-if="sliderstatus">
            <div class="align-items-center" :class="sliderstate">
                <label id="" class="font-wight-bold mr-2">MAX</label>
                <input type="number" class="form-control mx-2" style="width: 60px; text-align: center;" v-model="maxMount"
                    @change="$emit('update:maximum', maxMount)">
                <input type="range" class="custom-range" min="0" max="200" v-model="maxMount"
                    @input="$emit('update:maximum', maxMount)">
            </div>
        </div>
    </transition>
</template>
<script>
export default {
    name: "price-slider",
    data: function () {
        return {
            maxMount: 50,
        }
    },
    props: ["sliderstatus", "maximum"],
    computed: {
        sliderstate: function () {
            return this.sliderstatus ? 'd-flex' : 'd-none'
        }
    }
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
    transition: opacity all 1s ease-in-out;
}

.fade-enter,
.fade-leave-to {
    opacity: 0;
}</style>