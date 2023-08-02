<template>
  <div class="searchbar">
    <div class="searchbar__input">
      <input type="text" placeholder="Recherchez un livre">
    </div>
    <div class="searchbar__button" @click.prevent="openModalMsg">
      <i class="fa-solid fa-magnifying-glass"></i>
    </div>
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
export default {
  name: 'SearchBar',
  components: { ModalMsg },
  data () {
    return {
      isModalMsgOpen: false
    }
  },
  methods: {
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
<style>
  .searchbar {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .searchbar__input {
    width: 300px;
    height: 35px;
    border: 1px solid #444;
  }
  .searchbar__input input {
    width: 100%;
    height: 100%;
    border: none;
    padding: 0 10px;
    font-family: EditorCndn, sans-serif;
    color: #444;
  }
  .searchbar__input input::placeholder {
    color: #6C1B39;
    opacity: 0.6;
    font-family: EditorCndn, sans-serif;
  }
  .searchbar__button {
    width: 35px;
    height: 35px;
    background-color: #FFC773;
    border: 1px solid #444;
    color: #6C1B39;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
