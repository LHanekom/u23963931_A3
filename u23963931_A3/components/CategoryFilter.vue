<!--u23963931 Hanekom-->

<template>
    <select v-model="selectedCategory">
        <option value="">All Categories</option>
        <option 
            v-for="category in categories" 
            :key="category" 
            :value="category">
                {{ category }}
        </option>
    </select>   
</template>

<script>
    export default {
        props: {
            categories: {
                type: Array,
                required: true,
            },
        },
        data() {
            return {
                selectedCategory: "",
            };
        },
        watch: {
            selectedCategory(newValue) {
                this.$emit("update:selectedCategory", newValue);
            },
        },
    };
</script>

<style scoped>
    select {
        padding: 10px;
        width: 200px;
        border-radius: 5px;
        border: 1px solid #ccc;
        margin-bottom: 20px;
    }
</style>