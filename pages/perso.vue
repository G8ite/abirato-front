<template>
  <div class="personnal_space">
    <nav class="navigation" :class="{ sticky: isSticky, replaced: isReplaced }">
      <a href="/perso">Catalogue</a>
      <a href="/stats">Statistiques</a>
      <a href="/blog">Blog</a>
      <a href="/infos">Mes infos</a>
    </nav>
    <div class="userbook-add-div">
      <button class="userbook-add-button" @click.prevent="goToAddPage">
        <i class="fas fa-plus" />
      </button>
    </div>
    <UserBookCard
      v-for="book in books"
      :key="book.book.book_id"
      :title="book.book.title"
      :authors="book.book.authors"
      :status="book.status"
      :purchasePrice="book.purchase_price"
      :sellingPrice="book.selling_price"
      :themes="book.book.tags"
      :onEbay="book.on_ebay"
    />
  </div>
</template>
<script>
import axios from 'axios'
import { mapGetters } from 'vuex'
import UserBookCard from '@/components/UserBookCard.vue'
export default {
  name: 'PersonnalSpace',
  components: {
    UserBookCard
  },
  data () {
    return {
      token: null,
      books: [],
      isSticky: false,
      isReplaced: true
    }
  },
  mounted () {
    this.getBooks()
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    ...mapGetters('auth', ['getToken']),
    async getBooks () {
      this.token = this.getToken()
      try {
        const response = await axios.get('http://localhost:8000/api/auth/user_books/search/', {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        const data = response.data.data
        await Promise.all(data.map(async (book) => {
          const statusResponse = await axios.get(`http://localhost:8000/api/statuses/${book.status_id}`)
          const statusData = statusResponse.data
          book.status = statusData.data.name
        }))
        this.books = data
      } catch (error) {
        console.log(error)
      }
    },
    handleScroll () {
      const navigation = document.querySelector('.navigation')
      if (navigation) {
        if (this.isSticky && window.pageYOffset < navigation.offsetTop) {
          this.isReplaced = false
        }
        if (window.pageYOffset > navigation.offsetTop) {
          this.isSticky = true
        } else {
          this.isSticky = false
        }
      }
    },
    goToAddPage () {
      this.$router.push('/addUserBook')
    }
  }
}
</script>
<style scoped>
.personnal_space {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.userbook-add-div {
  display: flex;
  justify-content: flex-end;
  width: 100%;
}
.userbook-add-button {
  background-color: #6C1B39;
  border: none;
  border-radius: 50%;
  color: white;
  cursor: pointer;
  font-size: 24px;
  height: 48px;
  margin: 16px;
  width: 48px;
}
.navigation {
  width: 100%;
  border: 1px solid #6C1B39;
  display: flex;
  justify-content: space-between;
  background-color: white;
  z-index: 100;
}

.navigation.sticky {
  position: fixed;
  top: 0;
}
.navigation a {
  color: #6C1B39;
  flex: 1;
  text-align: center;
  padding: 8px 16px;
  text-decoration: none;
}
.navigation.replaced {
  position: relative;
}
</style>
