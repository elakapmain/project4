<script setup>
    import Header from './components/Header.vue';
    import Totals from './components/Totals.vue';
    import CartAdd from './components/CartAdd.vue';
    import CartList from './components/CartList.vue';

    import { computed, ref } from 'vue';

    const cartItems = ref([
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
    
    // Handle emits from form and buttons
    const handleAdd = (itemData) => {
        cartItems.value.push({
            id: generateID(),
            item: itemData.item,
            price: itemData.price,
            discount: itemData.discount,
        })

        console.log(cartItems.value)
    }

    const handleRemove = (id) => {
        cartItems.value = cartItems.value.filter((x) => x.id !== id)
    }

    const generateID = () => {
        return Math.floor(Math.random()*10000000)
    }
</script>

<template>
    <Header></Header>
    <div class="container">
        <Totals :total="cartTotal" :totalWithDiscounts="discountedTotal" :discounts="cartDiscounts"></Totals>
        <CartAdd @itemAdded="handleAdd"></CartAdd>
        <CartList :cartItems="cartItems" @itemRemoved="handleRemove"></CartList>
    </div>
</template>