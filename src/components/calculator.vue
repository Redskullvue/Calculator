<template>
  <div class="calculator">
    <div class="display">{{ display || "0" }}</div>
    <div class="btn" @click="clearbtn">C</div>
    <div class="btn">+/-</div>
    <div class="btn">%</div>
    <div class="btn op" @click="devide">/</div>
    <div class="btn" @click="displayValue(7)">7</div>
    <div class="btn" @click="displayValue(8)">8</div>
    <div class="btn" @click="displayValue(9)">9</div>
    <div class="btn op" @click="times">x</div>
    <div class="btn" @click="displayValue(4)">4</div>
    <div class="btn" @click="displayValue(5)">5</div>
    <div class="btn" @click="displayValue(6)">6</div>
    <div class="btn op" @click="minus">-</div>
    <div class="btn" @click="displayValue(1)">1</div>
    <div class="btn" @click="displayValue(2)">2</div>
    <div class="btn" @click="displayValue(3)">3</div>
    <div class="btn op" @click="add">+</div>
    <div class="btn zero" @click="displayValue(0)">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn op" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: "CalCulator",
  data() {
    return {
      display: "",
      operator: null,
      previous: null,
      operatorClick : false,
    };
  },
  methods: {
    setPrevious() {
      this.previous = this.display;
      this.operatorClick=true
    },
    displayValue(number) {
      if(this.operatorClick){
        this.display= ""
        this.operatorClick= false;
      }
      this.display = this.display + number;
    },
    clearbtn() {
      this.display = "";
    },
    dot() {
      if (this.display.indexOf(".") === -1) {
        this.displayValue(".");
      }
    },
    add() {
      this.operator = (a, b) =>a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    devide() {
      this.operator = (a, b) =>  a / b;
      this.setPrevious();
    },
    equal() {
      this.display =`${this.operator(parseFloat(this.previous), parseFloat(this.display))}`
    },
  },
};
</script>
<style scoped>
.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
  padding: 10px;
  text-align: center;
  box-shadow: 1px 1px 1px black;
  margin: 1px;
  border-radius: 5px;
}
.btn:hover{
  background-color : #d4cece
}
.zero {
  grid-column: 1/3;
}
.op {
  background-color: orange;
  color: white;
}
.op:hover{
  background-color:rgb(241, 110, 22) ;
}
.display {
  grid-column: 1/5;
  background-color: #333;
  text-align: center;
  color: white;
}
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 35px;
  font-weight: 100;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px auto);
}
</style>
