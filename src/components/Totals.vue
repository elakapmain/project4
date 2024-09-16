<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        total: {
            type: Number,
            require: true,
        },
        discounts: {
            type: Number,
            require: true,
        },
        totalWithDiscounts: {
            type: Number,
            require: true,
        }
    })
</script>

<template>
    <h3>Original Total</h3>
    <h2 class="totals">${{ total }}</h2>

    <h3>With Discounts</h3>
    <h2 class="totals">${{ totalWithDiscounts }}</h2>
    <h3 class="totals" id="savings" v-if="discounts > 0">You saved ${{ discounts }}!</h3>
</template>