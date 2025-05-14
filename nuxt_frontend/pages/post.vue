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
    <div v-else-if="error">
      <p>Error loading post: {{ error.message }}</p>
      <nuxt-link to="/">Back to Home</nuxt-link>
    </div>
    <div v-else>
      <p>Post not found or no documentId provided.</p>
      <nuxt-link to="/">Back to Home</nuxt-link>
    </div>
  </div>
</template>
<script setup>
    import { marked } from 'marked';
    import { useRoute, useRuntimeConfig, useAsyncData} from '#app';
    import { ref } from 'vue';

    const route = useRoute();
    const config = useRuntimeConfig();
    const documentId = ref(route.query.documentId);
    console.log('Rendering post page for documentId:', documentId);

    watch(() => route.query.documentId, (newDocumentId) => {
        documentId.value = newDocumentId;
    });

    const { data: post, error } = await useAsyncData(`post-${documentId.value}`, async () => {
        try {
            if (!documentId.value) {
                throw new Error('No documentId provided in query');
            }
            const response = await $fetch(`${config.public.strapiUrl}/api/blog-posts/${documentId.value}`);
            console.log('Single Post API Response:', JSON.stringify(response, null, 2));
            if (!response.data) {
                throw new Error('Post not found in API response');
            }
            const postData = response.data;
            return {
                id: postData.id,
                documentId: postData.documentId,
                title: postData.title,
                author: postData.author,
                content: postData.content?.[0]?.children?.[0]?.text,
                category: postData.category,
            };
        } catch (err) {
            console.error('Error fetching post:', err);
            throw new Error(`Failed to fetch post with documentId ${documentId.value}: ${err.message}`);
        }
    }, 
    {
        key: `post-${documentId.value}`,
        default: () => null,
    });

    const renderedContent = computed(() => (post.value ? marked(post.value.content) : ''));
</script>

<style scoped>
    .container {
        max-width: 800px;
        margin: 0 auto;
        padding: 2rem;
        background-color: #F5F5F5;
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    }

    .container h1 {
        font-size: 2.25rem;
        color: #333333;
        margin-bottom: 1rem;
    }

    .container p {
        font-size: 1rem;
        color: #333333;
        margin: 0.5rem 0;
        line-height: 1.6;
    }

    .container p strong {
        color: #2F4F4F;
    }

    .container :deep(p) {
        margin: 1rem 0;
        line-height: 1.6;
        color: #333333;
    }

    .container :deep(h2) {
        font-size: 1.5rem;
        color: #333333;
        margin: 1.5rem 0 1rem;
    }

    .container :deep(ul), .container :deep(ol) {
        margin: 1rem 0;
        padding-left: 2rem;
        color: #333333;
    }

    .container :deep(a) {
        color: #2F4F4F;
        font-weight: 500;
        text-decoration: underline;
    }

    .container :deep(a:hover) {
        color: #3D6B6B;
    }

    .container a {
        display: inline-block;
        margin-top: 1.5rem;
        font-weight: 600;
        padding: 0.5rem 1rem;
        background-color: #2F4F4F;
        color: #FFFFFF;
        border-radius: 4px;
        text-decoration: none;
        transition: background-color 0.3s ease;
    }

    .container a:hover {
        background-color: #3D6B6B;
        color: #FFFFFF;
    }
</style>