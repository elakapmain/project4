<script setup>
    import Header from './components/Header.vue';
    import Totals from './components/Totals.vue';
    import CartAdd from './components/CartAdd.vue';
    import CartList from './components/CartList.vue';

    import { computed, ref, onMounted } from 'vue';

    const cartItems = ref([]);

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

        saveToLocalStorage()
    }

    const handleRemove = (id) => {
        cartItems.value = cartItems.value.filter((x) => x.id !== id)

        saveToLocalStorage()
    }

    const generateID = () => {
        return Math.floor(Math.random()*10000000)
    }

    const saveToLocalStorage = () => {
        localStorage.setItem('cartItems', JSON.stringify(cartItems.value))    //  Same name as array
    }

    onMounted(() => {
        const savedCartItems = JSON.parse(localStorage.getItem('cartItems'))

        if(savedCartItems) {
            cartItems.value = savedCartItems
        }
    })
</script>

<template>
    <Header></Header>
    <div class="container">
        <Totals :total="cartTotal" :totalWithDiscounts="discountedTotal" :discounts="cartDiscounts"></Totals>
        <CartAdd @itemAdded="handleAdd"></CartAdd>
        <CartList :cartItems="cartItems" @itemRemoved="handleRemove"></CartList>
    </div>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');
</style>