<template>
  <div class="userbook-card">
    <div class="userbook-card__info">
      <div class="userbook-card_1">
        <div :class="['userbook-card__on-ebay', onEbay ? 'green' : 'red']" />
        <p class="userbook-card_status">
          {{ status }}
        </p>
        <div class="userbook-card__img">
          <img :src="imageUrl" alt="book cover" class="userbook-card__img-src">
        </div>
      </div>
      <div class="userbook-card_2">
        <h3 class="userbook-card__title">
          {{ title }}
        </h3>
      </div>
      <div class="userbook-card_3">
        <p class="userbook-card__author">
          {{ formattedAuthors }}
        </p>
      </div>
      <div class="userbook-card_5">
        <p class="userbook-card__selling-price">
          prix de vente :
          {{ formattedSellingPrice }}
        </p>
        <p class="userbook-card__purchase-price">
          prix d'achat :
          {{ formattedPurchasePrice }}
        </p>
      </div>
      <div class="userbook-card_4">
        <button class="userbook-card__button" @click.prevent="openModalMsg">
          Modifier
        </button>
        <button class="userbook-card__button" @click.prevent="openModalMsg">
          Supprimer
        </button>
      </div>
    </div>
    <div class="userbook-card__themes">
      <div v-for="theme in themes" :key="theme.id" class="userbook-card__theme">
        <p class="userbook-card__theme-text">
          {{ theme.tag_name }}
        </p>
      </div>
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
  name: 'UserBookCard',
  components: { ModalMsg },
  props: {
    id: {
      type: Number,
      default: 0
    },
    imageUrl: {
      type: String,
      default: 'https://i.ebayimg.com/images/g/ySYAAOSwi3lkfcGo/s-l1600.jpg'
    },
    title: {
      type: String,
      default: 'Null'
    },
    authors: {
      type: Array,
      default: () => []
    },
    status: {
      type: String,
      default: 'Null'
    },
    purchasePrice: {
      type: String,
      default: '0,00'
    },
    sellingPrice: {
      type: String,
      default: '0,00'
    },
    themes: {
      type: Array,
      default: () => []
    },
    onEbay: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      token: '',
      isModalMsgOpen: false
    }
  },
  computed: {
    formattedAuthors () {
      return this.authors.map(author => `${author.firstname} ${author.lastname}`).join(', ')
    },
    formattedPurchasePrice () {
      return this.purchasePrice + '€'
    },
    formattedSellingPrice () {
      return this.sellingPrice + '€'
    }
  },
  methods: {
    openModalMsg () {
      this.isModalMsgOpen = true
    },
    closeModalMsg () {
      this.isModalMsgOpen = false
    }
  }
}
</script>

<style scoped>
.userbook-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 16px 0;
  width: 100%;
}
.userbook-card__info {
  border: 1px solid #6C1B39;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 16px;
  width: 95%;
}
.userbook-card_1 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}
.userbook-card__on-ebay {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-right: 8px;
}

.userbook-card__on-ebay.green {
  background-color: green;
}

.userbook-card__on-ebay.red {
  background-color: red;
}

.userbook-card__img {
  display: none;
}

.userbook-card__img-src {
  max-width: 100%;
  max-height: 120px;
  margin-top: 8px;
}

.userbook-card_status {
  font-weight: bold;
  text-align: right;
}

.userbook-card__title {
  font-size: 18px;
  text-align: center;
  margin: 12px 0;
}

.userbook-card__author {
  font-style: italic;
  margin-bottom: 16px;
}
.userbook-card_3 {
  width: 100%;
  text-align: center;
}
.userbook-card_5 {
  display: flex;
  justify-content: space-around;
  width: 100%;
  margin-bottom: 16px;
}
.userbook-card__selling-price,
.userbook-card__purchase-price {
  font-weight: bold;
}
.userbook-card_4{
  display: flex;
  justify-content: space-around;
  width: 100%;
}
.userbook-card__button {
  background-color: #6C1B39;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
}

.userbook-card__theme {
  display: flex;
  justify-content: flex-end;
}

.userbook-card__theme-text {
  background-color: #FFC773;
  color: #444;
  padding: 4px 8px;
  margin-right: 8px;
  border: 1px solid #444;
}
.userbook-card__themes{
  display: flex;
  justify-content: flex-end;
  width: 100%;
  padding-right: 15px;
}
</style>
