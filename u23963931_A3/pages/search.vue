<!--u23963931 Hanekom-->

<template>
    <div class="container">
        <h1>Search Posts</h1>
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

<script>
    export default {
        data() {
            return {
                searchQuery: "",
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
            filteredPosts() {
                const query = this.searchQuery.toLowerCase();
                return this.posts.filter(
                    (post) =>
                    post.title.toLowerCase().includes(query) ||
                    post.author.toLowerCase().includes(query)
                );
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

    input { 
        width: 100%; 
        padding: 10px; 
        margin-bottom: 20px; 
    }

    .posts { 
        display: grid; 
        gap: 20px; 
    }
</style>