<script setup>
    import { ref, defineEmits } from 'vue';

    const item = ref('')

    // Strings will be parsed elsewhere
    const price = ref('')
    const discount = ref('')

    const emit = defineEmits([
        'itemAdded'
    ])

    const onSubmit = () => {
        const itemData = {
            item: item.value,
            price: Math.abs(parseFloat(price.value)),
            discount: checkBlank(discount.value)
        }
        
        emit('itemAdded', itemData)

        item.value = ''
        price.value = ''
        discount.value = ''
    }

    const checkBlank = (value) => {
        if (value === '')
            return 0
        else
            return parseFloat(value)
    }
</script>

<template>
    <h3>Add to cart</h3>

    <form id="form" @submit.prevent="onSubmit">
        <div class="form-segment">
            <label for="item">Enter product name</label>
            <input type="text" id="item" v-model="item" placeholder="Item name..." required>
        </div>
        <div class="form-segment">
            <label for="price">Enter item price</label>
            <input type="number" id="price" v-model="price" placeholder="Item price..." required>
        </div>
        <div class="form-segment">
            <label for="discount">Enter applicable discounts</label>
            <input type="number" id="discount" v-model="discount" placeholder="Leave blank if none...">
        </div>

        <button id="add-button" >Add to Cart</button>
    </form>
</template>