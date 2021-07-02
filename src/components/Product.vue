<template>
    <div class="card">
        <div class="img-box" :style="{ 'background-color': product.bgColor }">
            <img :src="require(`@/assets/img/products/${product.id}.svg`)">
        </div>
        <div class="text-block">
            <h5 class="category">{{product.category}}</h5>
            <h2 class="name">{{product.name}}</h2>
            <div class="flex-box">
                <div class="price">${{Number(product.price).toFixed()}}</div>
                <div class="btn_add-to-cart">
                    <span class="btn-text">{{isInCart ? '': 'Add'}}</span>
                    <span :id="`sub` + product.id" class="sub hidden" @click="sub()" v-on:remove-from-cart="removeFromCart($event)">
                      <img src="../assets/img/minus.svg" alt="-" />
                    </span>
                    <span :id="`counter` + product.id" class="counter1 hidden">{{itemCount}}</span>
                    <span :id="product.id" class="add" @click="$emit('add-to-cart',product); add(); showBtns()" :disabled="isInCart">
                       <img src="../assets/img/plus.svg" alt="+" />
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
   data () {
    return {
        itemCount: 0
    }
  },
  props: ['value','product','isInCart'],
  methods: {
    emitResult() {
      this.$emit('value', this.itemCount)
    },

    add() {
      this.itemCount += 1
      this.emitResult()
    },
    sub() {
      if(this.itemCount >= 1) {
          this.itemCount -= 1
          this.emitResult()
        }
    },
  },
  computed: {
    showBtns() {
        const counter2 = document.getElementById('counter2');
        counter2.classList.remove('hidden')
        const popUp = document.getElementById('pop-up');
        popUp.classList.remove('hide')

        const btn1 = document.getElementById('1')
        const btn2 = document.getElementById('2')
        const btn3 = document.getElementById('3')
        const btn4 = document.getElementById('4')
        const btn5 = document.getElementById('5')

        if(btn1) {
            document.getElementById('sub1').classList.remove('hidden');
            document.getElementById('counter1').classList.remove('hidden');
        }
        if(btn2){
            document.getElementById('sub2').classList.remove('hidden');
            document.getElementById('counter2').classList.remove('hidden');
        }
        if(btn3){
            document.getElementById('sub3').classList.remove('hidden');
            document.getElementById('counter3').classList.remove('hidden');
        }
        if(btn4){
            document.getElementById('sub4').classList.remove('hidden');
            document.getElementById('counter4').classList.remove('hidden');
        }
        if(btn5){
            document.getElementById('sub5').classList.remove('hidden');
            document.getElementById('counter5').classList.remove('hidden');
        }
    }
  } 
}
</script>

<style scoped>
.card {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 25px 5%;
    border-bottom: 1px #000 solid;
}
.text-block {
    width: 50vw;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.flex-box {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    min-height: 6vh;
    margin-top: 2vh;
}
.img-box {
    border: 2px #000 solid;
    border-radius: 20px;
    width: 27vw;
    height: auto;
    margin: 0 20px 0 0;
    padding-bottom: 20px;
}
.img-box img {
    width: 90%;
    height: auto;
    margin: 10% auto auto 5%;
}
.category {
    color: #999;
    font-size: 1rem;
    line-height: 100%;
    margin: 2px 0 0 0;
}
.name {
    margin: 0;
    line-height: 120%;
    max-width: 95%;
}
.price {
    font-size: 28px;
    margin-top: .5vh;
}
.btn_add-to-cart {
    height: 35px;
    width: 90px;
    padding-left: 10px;
    background-color: #FFBD12;
    border: 2px #000 solid;
    border-radius: 10px;
    text-align: left;
    font-size: 18px;
    font-family: "XBold", sans-serif;
}
.btn-text {
    position: absolute;
    margin-left: -27px;
    padding: 7px 10px 0 5px;
    z-index: 9;
    background-color: #FFBD12;
}
.add, .sub {
    background-color: #fff;
    width: 30px;
    height: 35px;
    padding: 0;
    cursor: pointer;
}
.sub {
    float: left;
    position: relative;
    left: -10px;
    z-index: 98;
    line-height: 45%;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
}
.counter1 {
    text-align: center;
    position: relative;
    top: 7px;
    padding-left: 6px;
}
.add {
    float: right;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    z-index: 99999;
}
</style>