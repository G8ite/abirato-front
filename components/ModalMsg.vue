<template>
  <div class="modal-overlay">
    <div class="modal-container">
      <div class="modal-header">
        <span class="modal-close" @click="close"><i class="fas fa-times" /></span>
      </div>
      <div class="modal-body">
        <h2 class="modal-title">{{ title }}</h2>
        <p class="modal-content">{{ content }}</p>
        <button class="modal-button" @click="close">
          {{ buttonMsg }}
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ModalMsg',
  props: {
    title: {
      type: String,
      required: true
    },
    content: {
      type: String,
      required: true
    },
    buttonMsg: {
      type: String,
      required: true
    }
  },
  methods: {
    close () {
      console.log('close')
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

.modal-title {
  font-family: 'EditorCndn', sans-serif;
  font-size: 24px;
  margin-bottom: 10px;
}

.modal-content {
  font-family: 'EditorCndn', sans-serif;
  font-size: 16px;
}

.modal-button {
  background-color: #6C1B39;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-family: 'EditorCndn', sans-serif;
  font-size: 16px;
  padding: 10px 20px;
  margin-top: 20px;
  width: 100%;
  text-align: center;
}

@media (max-width: 500px) {
  .modal-container {
    width: 90%;
  }
}
</style>
