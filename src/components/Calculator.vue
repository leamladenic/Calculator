<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="mult" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      prev: null,
      operatorClicked: false,
      current: "",
      operator: null
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = this.current + number;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrev() {
      this.prev = this.current;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrev();
    },
    mult() {
      this.operator = (a, b) => a * b;
      this.setPrev();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrev();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrev();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.prev),
        parseFloat(this.current)
      )}`;
      this.prev = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 60vh;
  margin: 0 auto;
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
  padding: 2vh;
  margin-top: 12vh;
  text-align: end;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #eee;
  border: 1px solid #999;
  padding: 15px;
  text-align: center;
  cursor: pointer;
}
.operator {
  background-color: #ad0068;
  color: white;
}
</style>
