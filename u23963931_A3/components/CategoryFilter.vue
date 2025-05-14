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
        width: 100%;
        max-width: 250px;
        padding: 0.75rem 1rem;
        margin-bottom: 25px;
        color: #999999;
        border: 1px solid #E0E0E0;
        border-radius: 4px;
        font-size: 1rem;
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
        background-color: #FFFFFF;
        cursor: pointer;
        transition: border-color 0.3s ease;
    }

    select:focus {
        outline: none;
        border-color: #2F4F4F;
        box-shadow: 0 0 0 3px rgba(47, 79, 79, 0.1);
    }
</style>