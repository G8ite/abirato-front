<template>
  <div class="hero">
    <h1>Ab Irato,</h1>
    <h2>Vente de livres anciens</h2>
    <div class="hero__searchbar">
      <SearchBar />
    </div>
  </div>
</template>
<script>
import SearchBar from '@/components/SearchBar.vue'
export default {
  name: 'HeroView',
  components: { SearchBar }
}
</script>

<style>

.hero{
  height: 250px;
  width: 100%;
  box-shadow: black 0px 0px 10px;
}

h1{
  font-size: 40px;
  font-family: Orbit, sans-serif;
  color: #6C1B39;
  text-align: center;
  padding-top: 30px;
}
h2{
  font-size: 20px;
  font-family: EditorCndn, sans-serif;
  color: #6C1B39;
  text-align: center;
  margin-bottom: 10px;
}
@media (min-width: 769px) {
  .hero{
    height: 400px;
  }
  h1{
    font-size: 60px;
    padding-top: 100px;
  }
  h2{
    font-size: 30px;
  }
}

</style>
