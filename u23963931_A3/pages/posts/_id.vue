<!--u23963931 Hanekom-->

<template>
    <div class="container">
        <div v-if="post">
            <h1>{{ post.title }}</h1>
            <p><strong>Author:</strong> {{ post.author }}</p>
            <p><strong>Category:</strong> {{ post.category }}</p>
            <div v-html="renderedContent"></div>
            <nuxt-link to="/">Back to Home</nuxt-link>
        </div>
        <div v-else>
            <p>Post not found.</p>
            <nuxt-link to="/">Back to Home</nuxt-link>
        </div>
    </div>
</template>

<script setup>
    import { marked } from 'marked';
    import { useRoute } from 'vue-router';

    const route = useRoute();
    const documentId = route.params.id;
    console.log('Rendering post page for ID:', documentId);

    const { data: post, error } = await useAsyncData(`post-${documentId}`, async () => {
    try {
        const response = await $fetch(`http://localhost:1337/api/blog-posts/${documentId}`);
        console.log('Single Post API Response:', JSON.stringify(response, null, 2));
        if (!response.data) {
        throw new Error('Post not found in API response');
        }
        const postData = response.data;
        return {
        id: postData.id,
        title: postData.title,
        author: postData.author,
        content: postData.content?.[0]?.children?.[0]?.text,
        category: postData.category,
        };
    } catch (err) {
        console.error('Error fetching post:', err);
        throw new Error(`Failed to fetch post with ID ${documentId}: ${err.message}`);
    }
    }, {
    key: `post-${documentId}`,
    default: () => null,
    });

    const renderedContent = computed(() => (post.value ? marked(post.value.content) : ''));
</script>

<style scoped>
    .container {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
    }
</style>