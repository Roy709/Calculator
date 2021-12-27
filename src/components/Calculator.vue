<template>
  <div>
    <h1>Calculator!</h1>
    <div class="calc">
      <div class="display">{{ current || "0" }}</div>
      <div @click="clear" class="btn">AC</div>
      <div @click="two" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="divide" class="btn sign">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="multiply" class="btn sign">*</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn sign">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn sign">+</div>
      <div @click="append(0)" class="btn zero">0</div>
      <div @click="del" class="btn">DEL</div>

      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn equal">=</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Calculator",

  setup() {
    let current = ref("");
    let previous = ref(null);
    let operator = ref(null);
    let operatorClick = ref(false);

    function clear() {
      current.value = "";
    }
    function two() {
      current.value =
        current.value.charAt(0) === "-"
          ? current.value.slice(1)
          : `-${current.value}`;
    }
    function percent() {
      current.value = `${current.value / 100}`;
    }
    function append(number) {
      if (operatorClick.value) {
        current.value = "";
        operatorClick.value = false;
      }
      current.value = `${current.value}${number}`;
    }
    function dot() {
      if (current.value.indexOf(".") === -1) {
        `${append(".")}`;
      }
    }
    function del() {
      current.value = current.value.slice(0, -1);
    }

    function setPrevious() {
      previous.value = current.value;
      operatorClick.value = true;
    }

    function divide() {
      operator.value = (a, b) => a / b;
      setPrevious();
    }

    function multiply() {
      operator.value = (a, b) => a * b;
      setPrevious();
    }

    function minus() {
      operator.value = (a, b) => a - b;
      setPrevious();
    }

    function add() {
      operator.value = (a, b) => a + b;
      setPrevious();
    }

    function equal() {
      current.value = operator.value(
        parseFloat(previous.value),
       parseFloat(current.value)
      );
      console.log(current.value);
      console.log(previous.value);

      previous.value=null;

    }

    return {
      current,  
      previous,
      operator,
      operatorClick,
      clear,
      two,
      percent,
      append,
      dot,
      del,
      setPrevious,
      divide,
      multiply,
      minus,
      add,
      equal,
    };
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  font-family: "Times New Roman", Times, serif;
}
.calc {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 30px;
  width: 400px;
  margin: 0 auto;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  text-align: center;
  border: 2px solid black;
  padding: 10px;
  border-radius: 10px;
}
.display {
  grid-column: 1/5;
  background-color: black;
  color: white;
  padding: 20px;
  text-align: center;
  border-radius: 15px;
  text-overflow: ellipsis;
  overflow: hidden;
}
.zero {
  /* grid-column: 1/3; */
  padding: 5px;
}
.btn {
  background-color: rgb(235, 232, 232);
  border: 1px solid rgb(128, 128, 128);
  padding: 5px;
  cursor: pointer;
  border-radius: 100px;
  margin-top: 10px;
  margin-left: 10px;
}
.btn:active {
  background-color: rgb(143, 143, 149);
}
.sign {
  background-color: orange;
  color: white;
  font-size: 40px;
}
.sign:active {
  background-color: darkgoldenrod;
}
.equal {
  background-color: rgb(0, 255, 234);
  color: rgb(0, 0, 0);
  font-size: 40px;
}
.equal:active {
  background-color: rgb(130, 195, 190);
}
</style>