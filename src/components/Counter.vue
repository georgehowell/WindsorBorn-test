<template>
  <div class="result">
   <input class="" :value="result"  readonly/>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: 0
    }
  },
  name: 'Counter',
  props: ['value'],
  methods: {
    updateValue() {
      this.$emit('input', this.result)
    }
  }
}
</script>

<style scoped>
input { 
    width: 20px;
    font-family: 'XBold';
    font-size: 20px;
    color: #000;
    text-align: center;
    position: relative;
    left: 4px;
    top: 4px;
    background-color: transparent;
    border-radius: 0;
    border: 0;
    padding: 0;
}
</style>