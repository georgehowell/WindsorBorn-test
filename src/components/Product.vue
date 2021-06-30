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
                    <Counter />
                    <span class="add" @click="$emit('add-to-cart',product); add(); showBtns()" :disabled="isInCart">
                       <img src="../assets/img/plus.svg" alt="+" />
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Counter from './Counter.vue'

export default {
   data () {
    return {
    }
  },
  props: ['value','product','isInCart'],
  components: {
    Counter
  },
  methods: {
    emitResult() {
      this.$emit('value', this.result)
    },
    add() {
      this.result += 1
      this.emitResult()
    },
    sub() {
        if(this.result >= 1) {
          this.result -= 1
          this.emitResult()
        }
    },
  },
    computed: {
        showBtns() {
            var minusBtn = document.getElementById('sub1');
            var counter1 = document.getElementById('counter1');
            var counter2 = document.getElementById('counter2');
            var popUp = document.getElementById('pop-up');
            if(counter1.value.length > 0) {
                minusBtn.classList.remove('hidden')
                counter1.classList.remove('hidden')
                counter2.classList.remove('hidden')
                popUp.classList.remove('hidden')
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
    width: 95px;
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
    z-index: 999;
    line-height: 45%;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
}
.counter1 {
    text-align: center;
    position: relative;
    top: 7px;
    padding-left: 3px;
}
.add {
    position: relative;
    top: -24px;
    float: right;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    z-index: 999;
}
</style>