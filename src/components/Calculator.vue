<template>
    <div class="calculator">
      <div class="display">{{current || '0'}}</div>
      <div @click="clear" class="clear">C</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="divide" class="btn operator">÷</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="times" class="btn operator">x</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="minus" class="btn operator">-</div>
      <div @click="append('0')" class="btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>
      <div @click="add" class="btn operator">+</div>


    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        previous: null,
        current: '',
        operator: null,
        operatorClicked: false,
      }
    },
    methods: {
      clear() {
        this.current = '';
      },
      sign() {
        this.current = this.current.charAt(0) === '-' ? 
          this.current.slice(1) : `-${this.current}`;
      },
      append(number) {
        if (this.operatorClicked) {
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`;
      },
      dot() {
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      setPrevious() {
        this.previous = this.current;
        this.operatorClicked = true;
      },
      divide() {
        this.operator = (a, b) => b / a;
        this.setPrevious();
      },
      times() {
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      minus() {
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },
      add() {
        this.operator = (a, b) => a + b;
        this.setPrevious();
      },
      equal() {
        this.current = `${this.operator(
          parseFloat(this.current), 
          parseFloat(this.previous)
        )}`;
        this.previous = null;
      }
    }
  }
  </script>
  
  <style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    background-color: white;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }
  .display {
    grid-column: 1 / 5;
    height: 12vmin;
    text-align-last: right;
    background-color: white;
    border: 1px solid black;
    margin: 1vmin;
    color: black;
  }
  .clear{
    grid-column: 4 / 5;
    background-color: rgb(255, 189, 189);
    border: 1px solid black;
    margin: 1vmin;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .btn {
    background-color: white;
    border: 1px solid black;
    margin: 1vmin;
  }
  .operator {
    background-color: rgb(228, 228, 228);
    color: black;
  }
  .equal{
    background-color: rgb(160, 241, 181);
  }
  </style>