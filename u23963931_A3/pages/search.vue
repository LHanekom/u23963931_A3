<!--u23963931 Hanekom-->

<template>
    <div class="container">
        <h1>Search</h1>
        <input 
            v-model="searchQuery" 
            placeholder="Search by title or author..."
            type="text"    
        />
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
    const searchQuery = ref('');

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
    }, 
    {
    key: 'posts',
        default: () => [],
    });

    const filteredPosts = computed(() =>
        posts.value.filter(
            post =>
            post.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
            post.author.toLowerCase().includes(searchQuery.value.toLowerCase())
        )
    );
</script>

<style scoped>
    .container {
        max-width: 800px;
        margin: 0 auto;
        padding: 2rem;
        background-color: #F5F5F5;
    }

    .container h1 {
        font-size: 2rem;
        color: #333333;
        margin-bottom: 1.5rem;
        text-align: center;
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    }

    input {
        width: 28%;
        padding: 0.8rem 1rem;
        margin: 0 auto;
        margin-bottom: 1.5rem;
        border: 1px solid #E0E0E0;
        border-radius: 4px;
        font-size: 1rem;
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
        transition: border-color 0.3s ease;
    }

    input:focus {
        outline: none;
        border-color: #2F4F4F;
        box-shadow: 0 0 0 3px rgba(47, 79, 79, 0.1);
    }

    input::placeholder {
        color: #999999;
    }

    .posts {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
        gap: 1.5rem;
    }
</style>