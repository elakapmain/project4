<script setup>
    import Header from './components/Header.vue';
    import Totals from './components/Totals.vue';
    import CartAdd from './components/CartAdd.vue';

    import { computed, ref } from 'vue';

    const cartItems = ref([
        {id: 1, name:'Text1', amount:250, discount: 20},
        {id: 1, name:'Text2', amount:250, discount: 20},
        {id: 1, name:'Text3', amount:250, discount: 20},
        {id: 1, name:'Text4', amount:250, discount: 20},
    ]);

    const cartDiscounts = computed(() =>{
        return cartItems.value.reduce((sum, x)=>{
            return sum+x.discount
        },0)
    })

    const cartTotal = computed(() =>{
        return cartItems.value.reduce((sum, x)=>{
            return sum+x.amount
        },0)
    })

    const discountedTotal = computed(() =>{
        return cartTotal.value - cartDiscounts.value
    })
</script>

<template>
    <Header></Header>
    <div class="container">
        <Totals :total="cartTotal" :totalWithDiscounts="discountedTotal" :discounts="cartDiscounts"></Totals>
        <CartAdd></CartAdd>
    </div>
</template>