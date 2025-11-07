<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const stage = ref('email') 
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const errorMessage = ref('')
const successMessage = ref('')

const handleEmailSubmit = () => {
  if (!email.value) {
    errorMessage.value = 'Por favor, insira seu email.'
    return
  }
  errorMessage.value = ''
  stage.value = 'reset'
}

const handlePasswordReset = () => {
  errorMessage.value = ''
  successMessage.value = ''

  if (!password.value || !confirmPassword.value) {
    errorMessage.value = 'Preencha todos os campos.'
    return
  }

  if (password.value !== confirmPassword.value) {
    errorMessage.value = 'As senhas não coincidem.'
    return
  }

  console.log('Senha redefinida para:', password.value)
  successMessage.value = 'Senha alterada com sucesso!'
  stage.value = 'success'
}
</script>

<template>
  <section class="login-container">
    <div class="login">
      <img src="/Logo.png" alt="Whisper" class="logo" />

      <!-- Etapa: inserir e-mail -->
      <template v-if="stage === 'email'">
        <h1>Esqueceu sua senha?</h1>
        <p>Insira o e-mail cadastrado para redefinir sua senha</p>

        <form @submit.prevent="handleEmailSubmit">
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

          <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>

          <button type="submit">Continuar</button>

          <div class="create-account">
            <RouterLink to="/login" class="create-link">
              Voltar ao Login
            </RouterLink>
          </div>
        </form>
      </template>

      <!-- Etapa: redefinir senha -->
      <template v-else-if="stage === 'reset'">
        <h1>Redefinir Senha</h1>
        <p>Crie uma nova senha para sua conta</p>

        <form @submit.prevent="handlePasswordReset">
          <div>
            <label for="password">Nova Senha:</label>
            <div class="input-group">
              <span class="mdi mdi-lock-outline"></span>
              <input
                type="password"
                id="password"
                v-model="password"
                required
                placeholder="Digite sua nova senha"
              />
            </div>
          </div>

          <div>
            <label for="confirmPassword">Confirmar Senha:</label>
            <div class="input-group">
              <span class="mdi mdi-lock-outline"></span>
              <input
                type="password"
                id="confirmPassword"
                v-model="confirmPassword"
                required
                placeholder="Confirme sua nova senha"
              />
            </div>
          </div>

          <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>

          <button type="submit">Salvar Nova Senha</button>

          <div class="create-account">
            <RouterLink to="/login" class="create-link">
              Voltar ao Login
            </RouterLink>
          </div>
        </form>
      </template>

      <template v-else-if="stage === 'success'">
        <h1>Senha Alterada!</h1>
        <p class="success-message">{{ successMessage }}</p>

        <div class="create-account">
          <RouterLink to="/login" class="create-link">
            Ir para o Login
          </RouterLink>
        </div>
      </template>
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
  height: 480px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  color: #fff;
  text-align: center;
}

.logo {
  display: block;
  margin: 0 auto 20px;
  width: 100px;
}

h1 {
  margin-bottom: 0;
  font-weight: bold;
  font-size: 2rem;
  color: #930000;
}

p {
  font-size: 0.8rem;
  margin-bottom: 25px;
  color: #B2B2B2;
}

.error-message {
  color: #AE0000;
  text-align: center;
  margin-bottom: 15px;
  font-size: 0.9rem;
}

.success-message {
  color: #7F7F7F;
  font-size: 1rem;
  margin-bottom: 25px;
}

form div {
  margin-bottom: 20px;
  text-align: left;
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

.create-link {
  display: inline-block;
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
