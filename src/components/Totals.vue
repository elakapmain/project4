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
    <h2 id="total">${{ total }}</h2>

    <h3>With Discounts</h3>
    <h2 id="applied">${{ totalWithDiscounts }}</h2>

    <h2 id="discounts">You saved ${{ discounts }}!</h2>
</template>