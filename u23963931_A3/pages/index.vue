<!--u23963931 Hanekom-->

<template>
    <div class="container">
        <h1>Blog Posts</h1>
        <CategoryFilter v-model="selectedCategory" :categories="categories" />
        <div class="posts">
            <PostCard
                v-for="post in filteredPosts"
                :key="post.id"
                :post="post"
            />
        </div>
    </div>
</template>

<script setup>
    const selectedCategory = ref('');

    const { data: posts, error } = await useAsyncData('posts', async () => {
    try {
        const response = await $fetch(`http://localhost:1337/api/blog-posts`, {
        params: {
            'fields[0]': 'title',
            'fields[1]': 'author',
            'fields[2]': 'content',
            'fields[3]': 'category',
        },
        });
        console.log('API Response:', JSON.stringify(response, null, 2));
        if (!response.data || !Array.isArray(response.data)) {
        throw new Error('Invalid response: data is not an array');
        }
        return response.data.map(post => {
        return {
            id: post.id,
            documentId: post.documentId,
            title: post.title,
            author: post.author,
            content: post.content?.[0]?.children?.[0]?.text,
            category: post.category,
        };
        }).filter(post => post !== null);
    } catch (err) {
        console.error('Error fetching posts:', err);
        return [];
    }
    }, {
    key: 'posts',
    default: () => [],
    });

    const categories = computed(() => [...new Set(posts.value.map(post => post.category))]);

    const filteredPosts = computed(() =>
    selectedCategory.value
        ? posts.value.filter(post => post.category === selectedCategory.value)
        : posts.value
    );
</script>

<style scoped>
    .container {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
    }
    .posts {
        display: grid;
        gap: 20px;
    }
</style>