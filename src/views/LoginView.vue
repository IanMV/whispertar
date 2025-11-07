<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const email = ref('')
const password = ref('')
const showPassword = ref(false)

const handleLogin = () => {
  console.log('Email:', email.value)
  console.log('Senha:', password.value)
}

const togglePassword = () => {
  showPassword.value = !showPassword.value
}
</script>

<template>
  <section class="login-container">
    <div class="login">
      <img src="/Logo.png" alt="Whisper" class="logo" />
      <h1>Bem-vindo de Volta</h1>
      <p>Entre na sua conta para melhorar sua experiência</p>

      <form @submit.prevent="handleLogin">
        <div>
          <label for="email">Email:</label>
          <div class="input-group">
            <span class="mdi mdi-email-outline"></span>
            <input
              type="email"
              id="email"
              v-model="email"
              required
              placeholder="exemplo@gmail.com"
            />
          </div>
        </div>

        <div>
          <label for="password">Senha:</label>
          <div class="input-group">
            <span class="mdi mdi-lock-outline"></span>
            <input
              :type="showPassword ? 'text' : 'password'"
              id="password"
              v-model="password"
              required
              placeholder="Digite sua senha"
            />
            <span
              :class="showPassword ? 'mdi mdi-eye-outline' : 'mdi mdi-eye-off-outline'"
              class="toggle-password"
              @click="togglePassword"
            ></span>
          </div>
        </div>

        <div class="options">
          <RouterLink to="/esqueci-senha" class="forgot-password">
            Esqueci minha senha
          </RouterLink>
        </div>

        <button type="submit">Entrar</button>

        <div class="create-account">
          <p>Não tem uma conta? <RouterLink to="/register" class="create-link">
            Criar conta
          </RouterLink></p>
          
        </div>
      </form>
    </div>
  </section>
</template>

<style scoped>
.login-container {
  height: 100vh;
  width: 100%;
  background: linear-gradient(to right, #0c0c0c, #0c0c0c 50%, transparent);
  display: flex;
  align-items: center;
  padding: 0;
}

.login {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  margin-left: 12%;
  padding: 20px;
  width: 420px;
  height: 550px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  color: #fff;
}

.logo {
  display: block;
  margin: 0 auto 20px;
  width: 100px;
}

h1 {
  text-align: center;
  margin-bottom: 0px;
  font-weight: bold;
  font-size: 2rem;
    color: #930000;
}

p {
  text-align: center;
  font-size: 0.8rem;
  margin-bottom: 25px;
  color: #b2b2b2;
}

form div {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  font-size: 1.1rem;
}

.input-group {
  position: relative;
  display: flex;
  align-items: center;
}

.input-group span.mdi {
  position: absolute;
  left: 10px;
  color: #7F7F7F;
  font-size: 1.2rem;
}

.input-group input {
  width: 100%;
  height: 40px;
  padding: 10px 40px 10px 35px;
  border-radius: 6px;
  border: 1px solid #333;
  background-color: #1a1a1a;
  color: white;
  outline: none;
  transition: 0.3s;
}

.input-group input:focus {
  border-color: #930000;
    box-shadow: #AE0000 0px 0px 8px;
}

.input-group span.toggle-password {
  position: absolute;
    left: 350px;
  cursor: pointer;
  color: #7F7F7F;
  font-size: 1.2rem;
  transition: color 0.3s;
}

.toggle-password:hover {
  color: #930000;
}

.options {
  display: flex;
  justify-content: flex-end;
  margin-top: -10px;
  margin-bottom: 20px;
}

.forgot-password {
  font-size: 0.85rem;
  color: #930000;
  text-decoration: none;
  transition: 0.3s;
}

.forgot-password:hover {
  text-decoration: underline;
    color: #AE0000;
    text-shadow: #AE0000 0px 0px 3px;
}

button {
  width: 100%;
  padding: 12px;
  background-color: #740000;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #930000;
  box-shadow: #ae0000 0px 0px 8px;
}

.create-account {
  text-align: center;
  margin-top: 5px;
}

.create-account p {
  margin: 0;
  color: #B2B2B2;
  font-size: 0.9rem;
}

.create-link {
  display: inline-block;
  margin-top: 5px;
  color: #930000;
  font-weight: 500;
  text-decoration: none;
  transition: 0.3s;
}

.create-link:hover {
  text-decoration: underline;
  color: #AE0000;
  text-shadow: #AE0000 0px 0px 3px;
}
</style>
