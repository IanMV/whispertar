<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import { RouterLink } from 'vue-router'

const showSearch = ref(false)
const searchQuery = ref('')
const searchInput = ref(null)
const lastScroll = ref(0)
const showHeader = ref(true)

const toggleSearch = async () => {
  showSearch.value = !showSearch.value
  if (showSearch.value) {
    await nextTick()
    searchInput.value?.focus()
  }
}

const handleClickOutside = (event) => {
  const searchArea = document.querySelector('.search-container')
  if (searchArea && !searchArea.contains(event.target)) {
    showSearch.value = false
  }
}

const handleScroll = () => {
  const currentScroll = window.scrollY
  if (currentScroll > lastScroll.value && currentScroll > 80) {
    showHeader.value = false
  } else {
    showHeader.value = true
  }
  lastScroll.value = currentScroll
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
  window.addEventListener('scroll', handleScroll)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header :class="{ hidden: !showHeader }">
    <div class="header-left">
      <h1>
        <RouterLink to="/">
          <img src="/Logo.png" alt="Logo" />
        </RouterLink>
      </h1>

      <nav>
        <ul>
          <li><RouterLink to="/">Início</RouterLink></li>
          <li><RouterLink to="/filmes">Filmes</RouterLink></li>
          <li><RouterLink to="/series">Séries</RouterLink></li>
          <li><RouterLink to="/detalhes">Destaques</RouterLink></li>
            <li><RouterLink to="/lista">Minha Lista</RouterLink></li>
        </ul>
      </nav>
    </div>

    <div class="header-right">
      <div class="search-container">
        <span class="mdi mdi-magnify" @click.stop="toggleSearch"></span>

        <input
          ref="searchInput"
          v-model="searchQuery"
          type="text"
          placeholder="Pesquisar..."
          class="search-input"
          :class="{ active: showSearch }"
        />
      </div>

      <RouterLink to="/login">
        <img src="/CaveiraLogin.svg" alt="Login" />
      </RouterLink>
    </div>
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 40px 0px 40px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(12, 12, 12, 0.259);
  transition: transform 0.4s ease, opacity 0.4s ease;
  z-index: 9999;
}

header.hidden {
  transform: translateY(-100%);
  opacity: 0;
}

.header-left {
  display: flex;
  align-items: center;
  background-color: transparent;
}

.header-left img {
  height: 50px;
}

nav ul {
  list-style: none;
  display: flex;
  gap: 20px;
  margin-left: 40px;
  padding: 0;
}

nav ul li {
  cursor: pointer;
  transition: all 0.3s ease;
}

nav ul li:hover {
  transform: scale(1.1);
}

nav ul li a {
  font-size: 1.03rem;
  text-decoration: none;
  color: #7f7f7f;
  font-weight: normal;
  transition: all 0.3s ease;
}

nav ul li:hover a {
  color: #930000;
  text-shadow: #AE0000 0px 0px 3px;
  text-decoration: underline;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 20px;
  position: relative;
}

.search-container {
  position: relative;
  display: flex;
  align-items: center;
}

.search-container .mdi-magnify {
  font-size: 1.5rem;
  color: #7f7f7f;
  cursor: pointer;
  transition: all 0.3s ease;
  position: absolute;
  left: 10px;
  z-index: 2;
  background-color: transparent;
}

.search-container .mdi-magnify:hover {
  color: #930000;
  transform: scale(1.2);
}

.search-input {
  padding: 8px 12px 8px 38px;
  font-size: 1rem;
  border-radius: 20px;
  border: 2px solid #930000;
  background-color: transparent;
  color: #b2b2b2 !important;
  outline: none;
  width: 0;
  opacity: 0;
  transition: all 0.3s ease;
}

.search-input.active {
  width: 400px;
  opacity: 1;
  border-color: #930000;
  box-shadow: #AE0000 0px 0px 8px;
}

.search-input.active ~ .mdi-magnify,
.search-container:has(.search-input.active) .mdi-magnify {
  color: #930000;
}

.search-input:focus {
  border-color: #930000;
}

.header-right img {
  height: 40px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.header-right img:hover {
  transform: scale(1.1);
  content: url('/CaveiraLoginVermelha.svg');
}
</style>
