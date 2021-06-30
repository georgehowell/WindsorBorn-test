<template>
  <div class="content">
    <ul class="list-group">
      <li class="list-group-item" v-for="item in items" :key="item.id" v-bind:style="{ backgroundColor: item.bgColor}" >
        <div class="left-block">
          <h4>{{ item.name }}</h4>
          <h3>${{ item.price }}</h3>
        </div>
        <button
          @click="$emit('remove-from-cart',item)"
          class="btn-close"
        ><img src="../assets/img/close.svg" alt="X" /></button>
      </li>
    </ul>
    <div class="card">
      <h2 class="total">${{total}}</h2>
    </div>
    <button class="btn-big" @click="goToCheckout()">Buy Now</button>
  </div>
</template>
<script>
export default {
  props: ["items"],
  page: "cart",
  methods: {
    goToCheckout() {
      document.getElementById('cart').classList.add('hidden') 
      document.getElementById('checkout').classList.remove('hidden') 
    },
  },
  computed: {
    total() {
      return this.items.reduce((acc, item) => acc + Number(item.price), 0);
    }
  }
};
</script>

<style scoped>
.content {
  width: calc(100% - 2vw);
  padding: 0 0 30px 0;
  margin: 0 0 0 -3vw;
}
.list-group {
  padding-right: 7.5%;
}
.list-group-item {
  width: 100%;
  height: 32vw;
  padding-left: 20px;
  margin-bottom: 12px;
  border-radius: 10px;
  border: 2px #000 solid;
  box-shadow: 0 2px 0 #000;
}
.left-block {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: -webkit-fill-available;
    width: 75%;
  padding: 22px 0 15px 0;
}
.list-group-item h4 {
    font-size: 22px;
    margin: 0;
    font-family: 'Bold', sans-serif;
    font-weight: 600;
}
.list-group-item h3 {
  font-size: 24px;
  margin: 10px 0 0 0;
}
.btn-close {
  float: right;
  position: relative;
  top: -32vw;
  text-align: center;
  width: 27px;
  height: 27px;
  margin: 2px;
  background-color: #fff;
  border-radius: 50%;
  box-shadow: 0 2px 0 #000;
  padding-top: 5px;
}
.btn-close img {
  width: 12px;
  height: auto;
  cursor: pointer;
}



.total {
    font-size: 8vw;
    float: left;
    margin: 20px 0 0 10%;
}
.btn-big {
    width: 150px;
    height: 55px;
    color: #fff;
    float: right;
    text-align: left;
    padding: 0 0 0 15px;
    background: #000 url(../assets/img/icon-chevron.svg) 92% center no-repeat;
    background-size: 10px;
    font-size: 20px;
    font-family: "XBold", sans-serif;
    margin: 20px 0 0 0;
    position: absolute;
    right: 7.5%;
}
.btn-big:hover {cursor: pointer;}


@media only screen 
  and (max-device-width: 420px) {
    .content { position: absolute; left: -5%;}
  }

</style>