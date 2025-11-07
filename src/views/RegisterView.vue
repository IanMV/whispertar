<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const name = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const showPassword = ref(false)
const errorMessage = ref('')

const handleRegister = () => {
  errorMessage.value = ''

  if (!name.value || !email.value || !password.value || !confirmPassword.value) {
    errorMessage.value = 'Preencha todos os campos.'
    return
  }

  if (password.value !== confirmPassword.value) {
    errorMessage.value = 'As senhas não coincidem.'
    return
  }

  console.log('Nome:', name.value)
  console.log('Email:', email.value)
  console.log('Senha:', password.value)

  alert('Conta criada com sucesso!')
}
</script>

<template>
  <section class="login-container">
    <div class="login">
      <img src="/Logo.png" alt="Whisper" class="logo" />
      <h1>Bem-vindo de Volta</h1>
      <p>Entre na sua conta para melhorar sua experiência</p>

      <form @submit.prevent="handleRegister">
        <div>
          <label for="name">Nome:</label>
          <div class="input-group">
            <span class="mdi mdi-account-outline"></span>
            <input
              type="text"
              id="name"
              v-model="name"
              required
              placeholder="Digite seu nome"
            />
          </div>
        </div>

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

        <div class="password-fields">
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
            </div>
          </div>
          <div>
            <label for="confirm-password">Confirmar Senha:</label>
            <div class="input-group">
              <span class="mdi mdi-lock-outline"></span>
              <input
                :type="showPassword ? 'text' : 'password'"
                id="confirm-password"
                v-model="confirmPassword"
                required
                placeholder="Confirme sua senha"
              />
            </div>
          </div>
        </div>

        <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>

        <button type="submit">Criar Conta</button>

        <div class="create-account">
          <RouterLink to="/login" class="create-link">
            Voltar ao Login
          </RouterLink>
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
  margin-top: 50px;
  padding: 20px;
  width: 420px;
  height: 600px;
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
  margin-bottom: 0;
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

.error-message {
  color: #AE0000;
  text-align: center;
  margin-bottom: 15px;
  font-size: 0.9rem;
}

form div {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  font-size: 1rem;
}

.input-group {
  position: relative;
  display: flex;
  align-items: center;
}

.input-group span.mdi {
  position: absolute;
  left: 10px;
  color: #7f7f7f;
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

.password-fields {
  display: flex;
  gap: 10px;
  margin: 0;
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
  box-shadow: #AE0000 0px 0px 8px;
}

.create-account {
  text-align: center;
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
