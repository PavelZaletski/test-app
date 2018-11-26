<template>
  <section class="test">
    <h2>Calculator</h2>
    <div class="wrapper">
      <input class="result"  type="text" v-model="result" disabled><br />
      <div class="numbers">
        <button data-id="c" v-on:click="reset">C</button>
        <button data-id="<" v-on:click="removeSymbol">&larr;</button>
        <button :data-id="item" v-for="item in map.numbers" v-on:click="handleNumberCLick">{{item}}</button>
        <button :data-id="item" v-for="item in map.operators.values" v-on:click="handleOperatorClick">{{item}}</button>
        <button data-id="=" class="result-btn" v-on:click="calculate">=</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'calculator',
  data() {
    return {
      result: '',
      items: ['', ''],
      currentIndex: 0,
      currentOperator: null,
      map: {
        numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, '.'],
        operators: {
          values: ['+', '-', '*', '/'],
          callbacks: {
            '+': (a, b) => +a + +b,
            '-': (a, b) => a - b, 
            '*': (a, b) => a * b, 
            '/': (a, b) => a / b, 
          }
        }
      }
    }
  },
  methods: {
    handleNumberCLick: function(e) {
      const newValue = this.items[this.currentIndex] + e.target.innerHTML;
      this.set(newValue);
    },
    set(value) {
      this.result = this.items[this.currentIndex] = value;
    },
    calculate: function() {
      const cb = this.map.operators.callbacks[this.currentOperator];
      const newValue = cb(...this.items).toString();
      this.currentIndex = 0;
      this.items[1] = '';
      this.set(newValue);
    },
    removeSymbol: function(e) {
      const newValue = this.result.slice(0, -1);
      this.set(newValue);
    },
    reset: function () {
      this.set('');
    },
    handleOperatorClick: function({target}) {
      this.currentOperator = target.innerHTML;
      this.currentIndex++;
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  .wrapper {
    position: relative;
    width: 300px;
    margin: 50px auto 0;
  }

  .numbers {
    display: flex;
    flex-wrap: wrap;
    width: 300px;
  }

  button {
    flex-basis: 25%;
    padding: 20px;
    font-size: 24px;
    order: 100;
  }

  .result {
    width: 100%;
    padding: 10px 2px;
    font-size: 16px;
  }

  .result.error {
    box-shadow: 0 0 0 1px red inset;
  }

  .error-msg {
    position: absolute;
    top: -25px;
    color: red;
    text-align: center;
    width: 100%;
  }

  button[data-id="c"] {
    order: 0;
    flex-basis: 50%;
  }

  button[data-id="<"] {
    order: 1;
  }

  button[data-id="/"] {
    order: 2;
  }

  button[data-id="1"] {
    order: 3;
  }

  button[data-id="2"] {
    order: 4;
  }

  button[data-id="3"] {
    order: 5;
  }

  button[data-id="*"] {
    order: 6;
  }

  button[data-id="4"] {
    order: 7;
  }

  button[data-id="5"] {
    order: 8;
  }

  button[data-id="6"] {
    order: 9;
  }

  button[data-id="-"] {
    order: 10;
  }

  button[data-id="7"] {
    order: 11;
  }

  button[data-id="8"] {
    order: 12;
  }

  button[data-id="9"] {
    order: 13;
  }

  button[data-id="+"] {
    order: 14;
  }

  button[data-id="."] {
    order: 15;
  }

  button[data-id="0"] {
    order: 16;
  }

  button[data-id="="] {
    order: 17;
    flex-basis: 50%;
  }

</style>
