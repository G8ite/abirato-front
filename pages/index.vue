<template>
  <div class="container">
    <div class="space" />
    <div class="news">
      <SectionTitle text="Nouveautés" />
      <BookCard
        v-for="book in books"
        :key="book.book.book_id"
        :title="book.book.title"
        :authors="book.book.authors"
        :publisher="book.book.editor"
        :year="book.book.parution_date"
      />
    </div>
    <div class="blog">
      <SectionTitle text="Actualités" color="#fff" />
      <ArticleCard />
      <ArticleCard />
      <ArticleCard />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ArticleCard from '../components/ArticleCard.vue'
import SectionTitle from '@/components/SectionTitle.vue'
import BookCard from '@/components/BookCard.vue'

export default {
  name: 'IndexPage',
  components: { BookCard, SectionTitle, ArticleCard },
  data () {
    return {
      books: []
    }
  },
  mounted () {
    this.lastBooks()
  },
  methods: {
    async lastBooks () {
      try {
        const response = await axios.get('http://localhost:8000/api/userbooks/last')
        const data = response.data

        const books = data.data
        await Promise.all(books.map(async (book) => {
          const editorResponse = await axios.get(`http://localhost:8000/api/editors/${book.book.editor_id}`)
          const editorData = editorResponse.data
          book.book.editor = editorData.data.editor_name
        }))
        this.books = books
      } catch (error) {
        console.error('Erreur lors de l\'appel à l\'API', error)
      }
    }
  }
}

</script>

<style scoped>
  .container{
    padding: 0;
    margin: 0;
  }
  .news, .blog{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .blog {
    background-color: #6C1B39;
  }
  .space {
    width: 100%;
    height: 10px;
    background-color: #6C1B39;
  }
</style>
