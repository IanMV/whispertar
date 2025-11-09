<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
  <footer>
      <RouterLink to="/">
        <img src="/Logo.png" alt="Logo">
      </RouterLink>
      <p>&copy; 2025 - Todos os direitos reservados</p>
  </footer>
</template>

<style scoped>
footer {
  color: #7f7f7f;
  text-align: center;
  padding: 20px;
  margin-top: 40px;
}
</style>
