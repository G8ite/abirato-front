<template>
  <div class="modal-overlay">
    <div class="modal-container">
      <div class="modal-header">
        <span class="modal-close" @click="close"><i class="fas fa-times" /></span>
      </div>
      <div class="modal-body">
        <div class="modal-buttons">
          <button class="modal-button" @click="showLoginForm">
            Connexion
          </button>
          <button class="modal-button" @click="showRegistrationForm">
            Inscription
          </button>
        </div>
        <div v-if="isLoginFormVisible" class="modal-content">
          <h2>Formulaire de Connexion</h2>
          <form>
            <div class="form-group">
              <label for="id">Identifiant</label>
              <input id="id" v-model="username" type="text" placeholder="zfeest@example.com">
            </div>
            <div class="form-group">
              <label for="password">Mot de passe</label>
              <input id="password" v-model="password" type="password" placeholder="password">
            </div>
            <button class="modal-button" @click.prevent="connect">
              Se connecter
            </button>
          </form>
          <p><a href="#">Mot de passe oublié</a></p>
        </div>
        <div v-else class="modal-content">
          <h2>Veuillez contacter l'administrateur</h2>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import { mapMutations } from 'vuex'
export default {
  name: 'ModalConnect',
  data () {
    return {
      isLoginFormVisible: true,
      username: '',
      password: ''
    }
  },
  methods: {
    showLoginForm () {
      this.isLoginFormVisible = true
    },
    showRegistrationForm () {
      this.isLoginFormVisible = false
    },
    ...mapMutations('auth', ['setToken']),
    async connect () {
      try {
        const response = await axios.post('http://localhost:8000/api/login', {
          email: this.username,
          password: this.password
        }, {
          headers: {
            'Content-Type': 'application/json'
          }
        })

        const token = response.data.access_token
        this.setToken(token)

        this.$router.push('/perso')
      } catch (error) {
        console.error('Utilisateur non trouvé.', error)
      }
    },
    close () {
      this.$emit('close')
    }
  }
}
</script>
<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-container {
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  width: 400px;
  max-width: 90%;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.modal-header {
  display: flex;
  justify-content: flex-end;
}

.modal-close {
  cursor: pointer;
  font-size: 18px;
}

.modal-body {
  margin-top: 20px;
}

.modal-buttons {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.modal-button {
  margin: 0 10px;
  padding: 10px 20px;
  background-color: #6C1B39;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.modal-content {
  margin-top: 20px;
}

.modal-content h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

.form-group {
  margin-bottom: 10px;
}

.form-group label {
  display: block;
  font-size: 16px;
  margin-bottom: 5px;
}

.form-group input[type="text"],
.form-group input[type="password"] {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

p {
  text-align: center;
  margin-top: 10px;
}

p a {
  color: #6C1B39;
  text-decoration: underline;
  cursor: pointer;
}

@media (max-width: 500px) {
  .modal-container {
    width: 90%;
  }
}
</style>
