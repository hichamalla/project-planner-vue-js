<script setup>
import { RouterLink, RouterView } from "vue-router";

</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>

  </header>

  <RouterView />
</template>
<style>
  body {
    background: #f2f2f2;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    max-width: 800px;
    margin: 0 auto;
    color: #555;
  }
  </style>