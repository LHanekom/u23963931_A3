<!--u23963931 Hanekom-->

<template>
    <div class="post_card">
        <h2>{{ post.title }}</h2>
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p>{{ post.content.substring(0, 100) }}...</p>
        <nuxt-link :to="`/posts/${post.documentId}`">Read more</nuxt-link>
    </div>
</template>

<script>
    export default {
        props: {
            post: {
                type: Object,
                required: true,
            },
        },
    };
</script>

<style scoped>
    .post_card {
        border: 1px solid #ccc;
        padding: 20px;
        margin: 10px 0;
        border-radius: 5px;
        background-color: #f9f9f9;
    }
    
</style>