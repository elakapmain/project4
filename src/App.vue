<script setup>
    import Header from './components/Header.vue';
    import Totals from './components/Totals.vue';
    import CartAdd from './components/CartAdd.vue';
    import CartList from './components/CartList.vue';

    import { computed, ref } from 'vue';

    const cartItems = ref([
        {id: 1, name:'Text1', price:250, discount: 20},
    ]);

    const cartDiscounts = computed(() =>{
        return cartItems.value.reduce((sum, x)=>{
            return sum+x.discount
        },0)
    })

    const cartTotal = computed(() =>{
        return cartItems.value.reduce((sum, x)=>{
            return sum+x.price
        },0)
    })

    const discountedTotal = computed(() =>{
        return cartTotal.value - cartDiscounts.value
    })
    
    const handleRemove = (id) => {
        cartItems.value = cartItems.value.filter((x) => x.id !== id)
    }
</script>

<template>
    <Header></Header>
    <div class="container">
        <Totals :total="cartTotal" :totalWithDiscounts="discountedTotal" :discounts="cartDiscounts"></Totals>
        <CartAdd></CartAdd>
        <CartList :cartItems="cartItems" @itemRemoved="handleRemove"></CartList>
    </div>
</template>