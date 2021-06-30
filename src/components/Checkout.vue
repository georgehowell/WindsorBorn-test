<template>
    <form id="form">
        <label>Your name</label>
        <input placeholder="e.g. Jane Doe" required/>
       
        <label>Your email</label>
        <input placeholder="e.g. jane@company.co" required/>

        <div class="switch_box">
            <input type="checkbox" class="switch_1" required/>
        </div>
        <p>I agree to the terms and conditions</p>
        <div style="clear:both"></div>

        <button class="btn-blue"
        @click="goToOrderConf()">Pay  ${{total}}</button>  <!-- "total" to do  -->

    </form>
</template>

<script>
export default {
methods: {
    goToOrderConf() {
        document.getElementById('checkout').classList.add('hidden')
        document.getElementById('order-conf').classList.remove('hidden') 
    }
  }
}
</script>

<style scoped>
form {
    padding: 0 5%;
}
label, input {
    width: calc(100% - 20px);
}
label {
    font-family: "Bold", sans-serif;
    font-size: 12px;
}
input {
    margin: 10px 0 20px 0;
    height: 50px;
    padding: 0 0 0 20px;
    font-size: 21px;
    font-family: "Bold", sans-serif;
}
input::placeholder {
    font-family: "Med", sans-serif;
}

p {
    font: 12px "Bold"; 
    padding-top: 7px;
    float: left;
}

.btn-blue {
    background-color: #1947E5;
    border-radius: 15px;
    width: 100%;
    height: 60px;
    color: #fff;
    font: 22px "Bold", sans-serif;
    margin: 15px auto 0 auto;
    cursor: pointer;
 }

/* Switch Specific Styles Start */

.switch_box{
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
  float: left;
}

input[type="checkbox"].switch_1{
  font-size: 30px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 60px;
  height: 34px;
  background-color: #E9E7FC;
  border-radius: 20px;
  position: relative;
  cursor: pointer;
  outline: none;
  -webkit-transition: all .2s ease-in-out;
  transition: all .2s ease-in-out;
  font-size: 75px;
  text-align: center;
  line-height: 43%;
  color: #E9E7FC;
  text-shadow: 0 0 6px #000;
  margin-right: 10px;
  float: left;
}
  
input[type="checkbox"].switch_1:checked{
  background-color: #FFBD12;
  color: #FFBD12;
}
  
input[type="checkbox"].switch_1:after{
  position: absolute;
  top: -10px;
  content: "•";
  width: 44px;
  height: 44px;
  border: 3px #000 solid;
  border-radius: 50%;
  background: #fff;
  -webkit-transform: scale(.7);
          transform: scale(.7);
  left: -10px;
  -webkit-transition: all .2s ease-in-out;
  transition: all .2s ease-in-out;
}

input[type="checkbox"].switch_1:checked:after{
  left: calc(100% - 40px);
}
/* Switch Specific Style End */


</style>