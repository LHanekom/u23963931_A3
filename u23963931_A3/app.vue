<!--u23963931 Hanekom-->

<template>
  <div>
    <header>
      <nav>
        <nuxt-link to="/">Home</nuxt-link>
        <nuxt-link to="/search">Search</nuxt-link>
      </nav>
    </header>
    <main>
      <NuxtPage />
    </main>
  </div>
</template>

<style scoped>
  header {
    background-color: #FFFFFF;
    padding: 1.5rem 2rem;
    border-bottom: 1px solid #E0E0E0;
    position: sticky;
    top: 0;
    z-index: 100;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  nav {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    gap: 2rem;
  }

  nav a {
    font-size: 1.1rem;
    font-weight: 600;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    text-decoration: none;
    color: #2F4F4F;
    transition: background-color 0.3s ease, color 0.3s ease;
  }

  nav a.router-link-active,
  nav a:hover {
    background-color: #2F4F4F;
    color: #FFFFFF;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    background-color: #F5F5F5;
  }
</style>