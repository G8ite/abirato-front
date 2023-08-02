<template>
  <div class="footer">
    <div class="footer__title">
      Ab Irato
    </div>
    <a class="footer__email" href="mailto:ab.irato.pro@gmail.com">ab.irato.pro@gmail.com</a>
    <a class="footer__phone" href="tel:+33">Téléphone</a>
    <div class="footer__divider" />
    <nav class="footer__nav">
      <ul>
        <li><a href="#">Mentions légales</a></li>
        <li><a href="#">Infos pratiques</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
    <div class="footer__divider" />
    <nav class="footer__social">
      <a href="#"><img src="../assets/img/instagram.png" alt="Instagram"></a>
      <a href="#"><img src="../assets/img/ebay.png" alt="eBay"></a>
    </nav>
  </div>
</template>
<script>
export default {
  name: 'FooterView'
}
</script>
<style>
  .footer {
    height: 300px;
    width: 100%;
    background-color: #444;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: EditorCndn, sans-serif;
  }
  .footer__title {
    color: #FFC773;
    font-size: 18px;
  }
  .footer__email,
  .footer__phone {
    color: #fff;
    text-decoration: underline;
    font-size: 18px;
    margin-top: 10px;
  }
  .footer__phone {
    text-decoration: none;
  }
  .footer__divider {
    height: 4px;
    width: 100px;
    background-color: #FFC773;
    margin: 10px 0;
  }
  .footer__nav ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .footer__nav li {
    margin-bottom: 10px;
  }
  .footer__nav a {
    color: #fff;
    font-size: 18px;
    text-decoration: none;
  }
  .footer__social {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }
  .footer__social a {
    margin-right: 10px;
  }
  .footer__social img {
    height: 30px;
    width: 30px;
  }
</style>
