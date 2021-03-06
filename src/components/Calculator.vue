<template>
  <div class="calc">
    <div class="screen">{{ screen || 0 }}</div>
    <div class="keys">
      <div class="button">
        <button @click="clear" class="btn">C</button>
      </div>
      <div class="button">
        <button @click="negative" class="btn">+/-</button>
      </div>
      <div class="button">
        <button @click="percent" class="btn">%</button>
      </div>
      <div class="button">
        <button @click="divide" class="btn btn-side">÷</button>
      </div>
      <div class="button">
        <button @click="append('7')" class="btn">7</button>
      </div>

      <div class="button">
        <button @click="append('8')" class="btn">8</button>
      </div>
      <div class="button">
        <button @click="append('9')" class="btn">9</button>
      </div>
      <div class="button">
        <button @click="times" class="btn btn-side">x</button>
      </div>
      <div class="button">
        <button @click="append('4')" class="btn">4</button>
      </div>
      <div class="button">
        <button @click="append('5')" class="btn">5</button>
      </div>

      <div class="button">
        <button @click="append('6')" class="btn">6</button>
      </div>
      <div class="button">
        <button @click="minus" class="btn btn-side">-</button>
      </div>
      <div class="button">
        <button @click="append('1')" class="btn">1</button>
      </div>
      <div class="button">
        <button @click="append('2')" class="btn">2</button>
      </div>
      <div class="button">
        <button @click="append('3')" class="btn">3</button>
      </div>

      <div class="button">
        <button @click="plus" class="btn btn-side">+</button>
      </div>
      <div class="button col0">
        <button @click="append('0')" class="btn">0</button>
      </div>
      <div class="button">
        <button @click="dot('.')" class="btn">.</button>
      </div>
      <div class="button">
        <button @click="equal" class="btn btn-side">=</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      previus: null,
      operatorClicked: false,
      screen: "",
      operator: null,
    };
  },
  methods: {
    setPrevius() {
      this.previus = this.screen;
      this.operatorClicked = true;
      this.screen = "";
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevius();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevius();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevius();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevius();
    },
    equal() {
      this.screen = this.operator(
        parseFloat(this.previus),
        parseFloat(this.screen)
      );
    },
    dot(dot) {
      if (this.screen.toString().indexOf(".") === -1) this.append(dot);
    },
    append(num) {
      this.screen += num;
    },
    clear() {
      this.screen = "";
    },
    negative() {
      if (this.screen < 0) {
        this.screen += 2 * -this.screen;
      } else if (this.screen == 0) {
        this.screen = "-";
      } else {
        this.screen -= 2 * this.screen;
      }
    },
    percent() {
      this.screen = this.screen / 100;
    },
  },
  created() {
    window.addEventListener("keydown", (e) => {
      if (e.key == "1") {
        this.append(1);
      } else if (e.key == "2") {
        this.append(2);
      } else if (e.key == "3") {
        this.append(3);
      } else if (e.key == "4") {
        this.append(4);
      } else if (e.key == "5") {
        this.append(5);
      } else if (e.key == "6") {
        this.append(6);
      } else if (e.key == "7") {
        this.append(7);
      } else if (e.key == "8") {
        this.append(8);
      } else if (e.key == "9") {
        this.append(9);
      } else if (e.key == "0") {
        this.append(0);
      } else if (e.key == "," || e.key == ".") {
        this.dot(".");
      } else if (e.key == "/") {
        this.divide();
      } else if (e.key == "*") {
        this.times();
      } else if (e.key == "-") {
        this.minus();
      } else if (e.key == "+") {
        this.plus();
      } else if (e.key == "Enter") {
        this.equal();
      } else if (e.key == "Delete") {
        this.clear();
      } else if (e.key == "Backspace") {
        if (this.screen.length > 0) {
          this.screen = this.screen.slice(0, -1);
        } else {
          return;
        }
      }
    });
  },
};
</script>
<style scoped>
.calc {
  border: 1px solid black;
  width: 31rem;
  height: auto;
}
.screen {
  background-color: rgb(34, 34, 34);
  height: 4.5rem;
  width: inherit;
  color: white;
  font-size: 50px;
  text-align: center;
  overflow: hidden;
}

.button {
  width: inherit;
  border: 0.5px solid rgb(54, 54, 54);
}
.keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 4rem;
}
.col0 {
  grid-column: 1/3;
}
.btn {
  width: 100%;
  height: 100%;
  font-size: 30px;
  border: none;
  outline: none;
  cursor: pointer;
}
.btn-side {
  background-color: rgb(253, 183, 53);
}
.btn-side:active {
  background-color: rgb(250, 162, 0) !important;
}
.btn:active {
  background-color: rgb(170, 169, 169);
}
</style>
