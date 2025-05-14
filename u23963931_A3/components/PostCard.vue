<template>
    <div class="post_card">
        <h2>{{ post.title }}</h2>
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p>{{ post.content.substring(0, 100) }}...</p>
        <nuxt-link :to="`/post?documentId=${post.documentId}`">Read more</nuxt-link>
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
        background-color: #FFFFFF;
        border: 1px solid #E0E0E0;
        padding: 1.5rem;
        border-radius: 8px;
        transition: transform 0.3s ease, box-shadow 0.3s ease;
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    }

    .post_card:hover {
        transform: translateY(-5px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .post_card h2 {
        font-size: 1.5rem;
        color: #333333;
        margin: 0 0 0.5rem;
    }

    .post_card p {
        font-size: 1rem;
        line-height: 1.5;
        color: #666666;
        margin: 0.5rem 0;
    }

    .post_card p strong {
        color: #2F4F4F;
    }

    .post_card a {
        display: inline-block;
        margin-top: 1rem;
        font-weight: 600;
        padding: 0.5rem 1rem;
        background-color: #2F4F4F;
        color: #FFFFFF;
        border-radius: 4px;
        text-decoration: none;
        transition: background-color 0.3s ease;
    }

    .post_card a:hover {
        background-color: #3D6B6B;
    }
</style>