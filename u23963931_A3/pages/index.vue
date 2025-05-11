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

<script>
    export default {
        data() {
            return {
                selectedCategory: "",
                posts: [
                    {
                        id: 1,
                        title: "Post 1",
                        author: "John Doe",
                        content: "This is the full content for post 1, a sample blog post.",
                        category: "Tech",
                    },
                    {
                        id: 2,
                        title: "Post 2",
                        author: "Jane Smith",
                        content: "This is the full content for post 2, another blog post.",
                        category: "Lifestyle",
                    },
                    {
                        id: 3,
                        title: "Post 3",
                        author: "John Doe",
                        content: "This is the full content for post 3, yet another post.",
                        category: "Tech",
                    }
                ],
            };
        },
        computed: {
            categories() {
            return [...new Set(this.posts.map((post) => post.category))];
            },
            filteredPosts() {
            return this.selectedCategory
                ? this.posts.filter((post) => post.category === this.selectedCategory)
                : this.posts;
            },
        },
    };
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