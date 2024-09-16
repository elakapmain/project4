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
    <ul id="cart">
        <li v-for="x in cartItems" v-bind:key="x.id">
            {{ x.item }}
            <span id="discount" v-if="x.discount > 0">-${{ x.discount }}</span>
            <span id="price">${{ x.price }} </span>
            <button @click="itemRemoved(x.id)" class="delete">X</button>
        </li>
    </ul>
</template>