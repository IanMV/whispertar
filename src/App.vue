<script setup>
import { RouterView } from 'vue-router';
import FooterComponent from '@/components/HeaderAndFooter/FooterComponent.vue';
import HeaderComponent from '@/components/HeaderAndFooter/HeaderComponent.vue';
</script>

<template>
  <HeaderComponent></HeaderComponent>
  <main>
    <RouterView></RouterView>
  </main>
  <FooterComponent></FooterComponent>
</template>