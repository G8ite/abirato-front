<template>
  <div class="book-card">
    <div class="book-card__image">
      <img :src="imageUrl" alt="Book Image">
    </div>
    <div class="book-card__details">
      <h2 class="book-card__title">
        {{ title }}
      </h2>
      <p class="book-card__author">
        {{ formattedAuthors }}
      </p>
      <p class="book-card__publisher">
        {{ publisher }}
      </p>
      <p class="book-card__year">
        {{ year }}
      </p>
    </div>
    <div class="book-card__links">
      <a :href="bookLink" class="book-card__link">+ de détails</a>
    </div>
  </div>
</template>
<script>
export default {
  name: 'BookCard',
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
      default: 'Titre du livre'
    },
    authors: {
      type: Array,
      default: () => []
    },
    publisher: {
      type: String,
      default: 'Editeur'
    },
    year: {
      type: String,
      default: 'Année'
    },
    bookLink: {
      type: String,
      default: '#'
    }
  },
  computed: {
    formattedAuthors () {
      return this.authors.map(author => `${author.firstname} ${author.lastname}`).join(', ')
    }
  }
}
</script>
<style scoped>
.book-card {
  width: 280px;
  min-height: 350px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.25);
  overflow: hidden;
  padding: 20px;
  margin-bottom: 20px;
}
.book-card__image {
  width: 100%;
  height: 160px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.book-card__image img {
  width: 230px;
  height: 160px;
  object-fit: cover;
}
.book-card__details {
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
}
.book-card__title {
  color: #601833;
  font-family: EditorCndn, sans-serif;
  font-size: 18px;
  margin-bottom: 8px;
}
.book-card__author,
.book-card__publisher,
.book-card__year {
  color: #444;
  font-family: EditorCndn, sans-serif;
  font-size: 18px;
  margin-bottom: 8px;
  text-align: right;
}
.book-card__link {
  width: 100%;
  display: flex;
  justify-content: flex-start;
}
.book-card__link {
  color: #6C1B39;
  text-decoration: underline;
  font-family: EditorCndn, sans-serif;
  font-size: 18px;
}
</style>
