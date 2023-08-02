<template>
  <div class="app">
    <HeaderView />
    <HeroView />
    <Nuxt />
    <FooterView />
  </div>
</template>

<script>
import FooterView from '../components/FooterView.vue'
import HeroView from '../components/HeroView.vue'
import HeaderView from '@/components/HeaderView.vue'
import '@fortawesome/fontawesome-free/css/all.css'

export default {
  name: 'DefaultLayout',
  components: { HeaderView, HeroView, FooterView }
}
</script>
<style>
@font-face {
    font-family: 'Orbit';
    src: url('../assets/font/Orbit-Regular.ttf') format('truetype');
  }
@font-face {
    font-family: 'EditorCndn';
    src: url('../assets/font/EditorCndn.woff') format('woff');
}

</style>
