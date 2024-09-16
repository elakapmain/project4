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
        }
    })
</script>

<template>
    <h3>Cart Totals</h3>

    <h2 id="total">{{ total }}</h2>
    <h2 id="discounts">{{ discounts }}</h2>
</template>