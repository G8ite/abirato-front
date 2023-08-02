<template>
  <div class="header" :class="{ 'mobile-menu-open': isMobileMenuOpen }">
    <div class="header_logo-container">
      <a href="/">
        <div class="header_img">
          <img src="../assets/img/logo.png" alt="logo" :style="{ width: isMobile ? '40px' : 'auto' }">
        </div>
      </a>
    </div>
    <div class="header_nav" :style="{ display: isMobileMenuOpen || !isMobile ? 'block' : 'none' }">
      <div class="close-menu">
        <i v-if="isMobileMenuOpen" class="fas fa-times" @click="toggleMobileMenu" />
      </div>
      <ul>
        <li><a href="#">Accueil</a></li>
        <li><a href="#" @click.prevent="openModalMsg">Catalogue</a></li>
        <li><a href="#" @click.prevent="openModalMsg">Boutique Ebay</a></li>
        <li><a href="#" @click.prevent="openModalMsg">Articles</a></li>
        <li><a href="#" @click.prevent="openModalMsg">Infos pratiques</a></li>
        <li><a href="#" @click.prevent="openModalMsg">Contact</a></li>
        <li><a href="#" @click="openModal">Mon compte</a></li>
      </ul>
    </div>
    <div class="burger-menu-icon" @click="toggleMobileMenu">
      <i class="fas fa-bars" />
    </div>
    <ModalConnect v-if="isModalOpen" @close="closeModal" />
    <ModalMsg
      v-if="isModalMsgOpen"
      title="En construction"
      content="Cette page est en construction."
      buttonMsg="Fermer"
      @close="closeModalMsg"
    />
  </div>
</template>

<script>
import ModalMsg from '@/components/ModalMsg.vue'
import ModalConnect from '@/components/ModalConnect.vue'
export default {
  name: 'HeaderView',
  components: { ModalConnect, ModalMsg },
  data () {
    return {
      isMobile: false,
      isMobileMenuOpen: false,
      isModalOpen: false,
      isModalMsgOpen: false
    }
  },
  mounted () {
    this.checkMobile()
    window.addEventListener('resize', this.checkMobile)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.checkMobile)
  },
  methods: {
    checkMobile () {
      this.isMobile = window.innerWidth <= 768
    },
    toggleMobileMenu () {
      this.isMobileMenuOpen = !this.isMobileMenuOpen
    },
    openModal () {
      this.isMobileMenuOpen = false
      this.isModalOpen = true
    },
    closeModal () {
      this.isModalOpen = false
    },
    openModalMsg () {
      this.isModalMsgOpen = true
      this.isMobileMenuOpen = false
    },
    closeModalMsg () {
      this.isModalMsgOpen = false
    }
  }
}
</script>

<style scoped>
.header {
  background-color: #6C1B39;
  height: 80px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.header_img {
  width: 50px;
  height: 50px;
  background-color: #444;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 10px;
}
.header_logo-container {
  flex-grow: 1;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
.header_img img {
  max-width: 50px;
  max-height: 50px;
  background-color: #444;
}

.header_nav {
  position: absolute;
  top: 100%;
  right: 0;
  width: 100%;
  background-color: #fff;
  text-align: center;
  padding-top: 10px;
  z-index: 99;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  overflow-y: hidden;
}

.header_nav ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.header_nav li {
  margin: 10px 0;
}

.header_nav a {
  color: #6C1B39;
  font-family: 'Orbit', sans-serif;
  font-size: 18px;
  margin-bottom: 10px;
  text-decoration: none;
}
.burger-menu-icon {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-left: auto;
  padding-right: 10px;
}
.burger-menu-icon i {
  font-size: 30px;
  color: #fff;
  cursor: pointer;
}

.close-menu {
  display: flex;
  width: 100%;
  justify-content: flex-end;
  padding-right: 10px;
}

.close-menu i {
  font-size: 30px;
  color: #6C1B39;
  cursor: pointer;
}

@media (min-width: 769px) {
  .header {
    height: 100px;
  }

  .header_img {
    width: 100px;
    height: 100px;
  }

  .header_nav {
    position: static;
    width: auto;
    background-color: transparent;
    padding-top: 0;
  }

  .header_nav ul {
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  .header_nav li {
    margin-left: 20px;
  }

  .header_nav a {
    margin-bottom: 0;
    color: #fff;
  }
  .burger-menu-icon {
    display: none;
  }
}
</style>
