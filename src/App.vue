<template>
  <div id="app">
    <Shop />
  </div>
</template>

<script>
import Shop from "@/components/Shop.vue"
export default {
  components: {
    Shop
  }
}
</script>


<style>
@font-face {
    font-family: "XBold";
    src: url(assets/fonts/Montserrat-ExtraBold.ttf);
}
@font-face {
    font-family: "Bold";
    src: url(assets/fonts/Montserrat-Bold.ttf);
}
@font-face {
    font-family: "Med";
    src: url(assets/fonts/Montserrat-Medium.ttf);
}
  
h1, h2, h3, h4, h5, .price {
    font-family: "XBold", sans-serif;
    font-weight: 900;
}
h1 {
    font-size: 6vw;
    line-height: 110%;
    margin-left: 5%;
}
label {
    font-family: "Med", sans-serif;
}

input, button {
    border-radius: 12px;
    border: 2px #000 solid;
}
html, body {
  margin: 0;
  padding: 0;
}

#app {
  padding: 0;
  margin: 0;
  font-family: "Med", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
ul li {
  list-style: none;
}

.hidden { visibility: hidden;}
.hide {display:none;}

#counter2 .result input {
  position: relative;
  top: 0;
  left: 0;
  font-size: 14px;
}

</style>
