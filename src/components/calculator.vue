<template>
  <section class="test">
    <h2>Calculator</h2>
    <div class="wrapper">
      <div class="error-msg" v-if="hasError">Error occured</div>
      <input :class="{error : hasError, result: true}"  type="text" v-model="result" disabled><br />
      <div class="numbers" v-on:click="add">
        <button v-on:click="reset">C</button>
        <button>(</button>
        <button>)</button>
        <button v-on:click="removeSymbol">&larr;</button>
        <button>7</button>
        <button>8</button>
        <button>9</button>
        <button> / </button>
        <button>4</button>
        <button>5</button>
        <button>6</button>
        <button> * </button>
        <button>1</button>
        <button>2</button>
        <button>3</button>
        <button> - </button>
        <button>.</button>
        <button>0</button>
        <button class="result-btn" v-on:click="calculate">=</button>
        <button>+</button>
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
      hasError: false
    }
  },
  methods: {
    add: function(e) {
      this.result += e.target.innerHTML;
    },
    calculate: function(e) {
      e.stopPropagation();
      try {
        this.result = eval(this.result);
        this.hasError = false;
      } catch(e) {
        this.hasError = true;
      }
    },
    removeSymbol: function(e) {
      e.stopPropagation();
      this.result = this.result.slice(0, -1);
    },
    reset: function () {
      e.stopPropagation();
      this.result = '';
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

</style>
