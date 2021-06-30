<template>
  <div class="container">
    <h1>Order Confirmation</h1>
    <div class="content">
      <div class="box">
        <h3>Your order has<br />been processed</h3>
        <p>Your order ID is <strong>#102022</strong></p>
      </div>
        <button class="btn-black" 
          @click="goToShop()">Return to Products</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
      goToShop() {
          this.page = 'home';
          // document.getElementById('order-conf').classList.add('hidden') 
          location.reload();
      }
  }
}
</script>

<style scoped>
.content {
    padding: 0 5%;
}
.box {
  height: fit-content;
  margin: 10vw 0 20px 0;
  padding: 28% 0 10px 5%;
  border: 2px #000 solid;
  box-shadow: 0 5px #000;
  border-radius: 15px;
  background:url('../assets/img/bg_order-conf.svg') top center no-repeat;
  background-size: cover;
}

.btn-black {
    background-color: #000;
    border-radius: 15px;
    width: 100%;
    height: 60px;
    color: #fff;
    font: 22px "Bold", sans-serif;
    margin: 15px auto 0 auto;
    cursor: pointer;
 }

</style>