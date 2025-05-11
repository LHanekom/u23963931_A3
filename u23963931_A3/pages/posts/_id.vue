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

<script>
    import { marked } from 'marked';

    export default {
        data() {
            return {
                post: null,
            };
        },
        computed: {
            renderedContent() {
                return this.post ? marked(this.post.content) : '';
            },
        },
        async created() {
            const id = this.$route.params.id;
            const posts = [
                {
                    id: '1',
                    title: 'Post 1',
                    author: 'John Doe',
                    content: '# Post 1\nThis is the **full content** for post 1, a sample blog post.',
                    category: 'Tech',
                },
                {
                    id: '2',
                    title: 'Post 2',
                    author: 'Jane Smith',
                    content: '# Post 2\nThis is the **full content** for post 2, another blog post.',
                    category: 'Lifestyle',
                },
                {
                    id: '3',
                    title: 'Post 3',
                    author: 'John Doe',
                    content: '# Post 3\nThis is the **full content** for post 3, yet another post.',
                    category: 'Tech',
                },
            ];
            this.post = posts.find((post) => post.id === id) || null;
        },
    };
</script>

<style scoped>
    .container {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
    }
</style>