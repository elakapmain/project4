<script setup>
    import { defineProps, defineEmits } from 'vue';

    const props = defineProps({
        cartItems: {
            type: Array,
            require: true,
        }
    })

    const emit = defineEmits(['itemRemoved'])

    const itemRemoved = (id) => {
        emit('itemRemoved', id)
    }
</script>

<template>
    <h3>In your cart</h3>
    <ul id="cart"></ul>
        <li v-for="x in cartItems" v-bind:key="x.id">
            {{ x.item }} ${{ x.price }} -${{ x.discount }}
            <button @click="itemRemoved(x.id)" class="delete-btn">X</button>
        </li>
</template>