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
    background-color: #f4f4f4;
    padding: 10px 20px;
    border-bottom: 1px solid #ccc;
  }

  nav ul {
    list-style: none;
    padding: 0;
    display: flex;
    gap: 20px;
  }

  nav ul li {
    display: inline;
  }

  nav ul li a {
    text-decoration: none;
    color: #333;
    font-weight: bold;
  }

  nav ul li a:hover {
    color: #007bff;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }
  
</style>