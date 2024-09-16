<script setup>

</script>

<template>
    <h3>Add to cart</h3>

    <form id="form" @submit.prevent="onSubmit">
        <div class="form-segment">
            <label for="item">Enter product name</label>
            <input type="text" id="item" v-model="item" placeholder="Item name...">
        </div>
        <div class="form-segment">
            <label for="price">Enter item price</label>
            <input type="text" id="price" v-model="price" placeholder="Item price...">
        </div>
        <div class="form-segment">
            <label for="discounts">Enter applicable discounts</label>
            <input type="text" id="discounts" v-model="discounts" placeholder="Leave blank if none...">
        </div>

        <button class="button">Add to Cart</button>
    </form>
</template>