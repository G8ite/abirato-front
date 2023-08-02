<template>
  <div class="section-title">
    <div class="section-title__rectangle" />
    <div class="section-title__text" :style="{color:color}">
      {{ text }}
    </div>
  </div>
</template>
<script>
export default {
  name: 'SectionTitle',
  props: {
    text: {
      type: String,
      default: 'Titre de la section'
    },
    color: {
      type: String,
      default: '#6C1B39'
    }
  }
}
</script>
<style>
  .section-title {
    width: 100%;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    margin-bottom: 20px;
    padding-right: 10px;
  }
  .section-title__rectangle {
    width: 15px;
    height: 5px;
    background-color: #FFC773;
    border: 1px solid #444;
  }
  .section-title__text {
    margin-left: 20px;
    font-size: 26px;
    font-family: Orbit, sans-serif;
  }
</style>
