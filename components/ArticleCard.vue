<template>
  <div class="article-card">
    <div class="article-card__image">
      <img :src="imageUrl" alt="Image de l'article">
    </div>
    <div class="article-card__details">
      <h2 class="article-card__title">
        {{ title }}
      </h2>
      <p class="article-card__extract">
        {{ extract }}
      </p>
    </div>
    <div class="article-card__links">
      <div class="article-card__link">
        <i class="fa-solid fa-angle-right"></i>
        <a :href="articleLink">Lire l'article</a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ArticleCard',
  props: {
    imageUrl: {
      type: String,
      default: 'https://i.ebayimg.com/images/g/ySYAAOSwi3lkfcGo/s-l1600.jpg'
    },
    title: {
      type: String,
      default: 'Titre de l\'article'
    },
    extract: {
      type: String,
      default: 'Extrait de l\'article'
    },
    articleLink: {
      type: String,
      default: '#'
    }
  }
}
</script>
<style scoped>
  .article-card {
    width: 280px;
    height: 350px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.25);
    overflow: hidden;
    padding: 20px;
    margin-bottom: 20px;
    position: relative;
  }
  .article-card__image {
    width: 100%;
    height: 160px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .article-card__image img {
    width: 230px;
    height: 100%;
    object-fit: cover;
  }
  .article-card__details {
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
  }

  .article-card__title {
    color: #601833;
    font-family: EditorCndn, sans-serif;
    font-size: 18px;
    margin-bottom: 8px;
  }

  .article-card__extract {
    color: #444;
    font-family: EditorCndn, sans-serif;
    font-size: 18px;
    margin-bottom: 8px;
  }

  .article-card__links {
    width: 100%;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position: absolute;
    bottom: 10px;
    right: 10px;
  }
  .article-card__link {
    width: 100px;
    height: 30px;
    background-color: #FFC773;
    color: #444;
    font-family: EditorCndn, sans-serif;
    font-size: 14px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .article-card__link a {
    color: #444;
    text-decoration: none;
    margin-left: 10px;
  }
</style>
