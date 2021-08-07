<template>
  <div class="calculator">
    <div class="display">
      <div class="input">
        {{ input }}
      </div>
      <div class="output">
        {{ output }}
      </div>
    </div>
    <div class="row-1">
      <div class="button" id="ac" @click="clear">AC</div>
      <div class="button" id="ac" @click="cancel">&larr;</div>
      <div class="button" id="div" @click="enter('%')">%</div>
      <div class="button" id="div" @click="enter('/')">/</div>
    </div>
    <div class="row-2">
      <div class="button" @click="enter(7)">7</div>
      <div class="button" @click="enter(8)">8</div>
      <div class="button" @click="enter(9)">9</div>
      <div class="button" id="div" @click="enter('*')">*</div>
    </div>
    <div class="row-3">
      <div class="button" @click="enter(4)">4</div>
      <div class="button" @click="enter(5)">5</div>
      <div class="button" @click="enter(6)">6</div>
      <div class="button" id="div" @click="enter('-')">-</div>
    </div>
    <div class="row-4">
      <div class="button" @click="enter(1)">1</div>
      <div class="button" @click="enter(2)">2</div>
      <div class="button" @click="enter(3)">3</div>
      <div class="button" id="div" @click="enter('+')">+</div>
    </div>
    <div class="row-5">
      <div class="button" @click="enter(0)">0</div>
      <div class="button" @click="enter('.')">.</div>
      <div class="button equal" id="div" @click="equal">=</div>
    </div>
  </div>
</template>
<script>
export default {
  components: "Calculator",
  data() {
    return {
      input: "",
      output: "",
      calculated: false,
    };
  },
  methods: {
    clear() {
      this.input = "";
      this.output = "";
    },
    cancel() {
      const arr = this.input.split("");
      arr.pop();
      this.input = arr.join("");
    },
    enter(keys) {
      if (!this.calculated) {
        this.input += keys;
      } else {
        this.calculated = false;
        this.input = "";
        this.output = "";
        this.input += keys;
      }
    },
    equal() {
      if (this.input.includes("%")) {
        const arr = this.input.split("");
        const newArr = [];
        for (let i = 0; i < arr.length; i++) {
          if (arr[i] != "%") {
            newArr.push(arr[i]);
          } else {
            newArr.push("/100");
          }
        }
        this.input = newArr.join("");
        console.log(newArr);
      }
      console.log(this.input);
      this.output = eval(this.input);
      this.calculated = true;
    },
  },
};
</script>
<style scoped>
.calculator {
  min-width: 300px;
  background-color: black;
  border: 1px solid black;
  border-radius: 10px;
  display: flex;
  font-size: 24px;
  width: 25%;
  height: 32rem;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding: 5px;
  margin: 60px 0px;
}
.display {
  min-width: 300px;
  width: 20%;
  margin: auto;
  text-align: right;
  height: 80px;
  cursor: pointer;
  border-radius: 5px;
  background-color: black;
}

.button {
  width: 20%;
  height: 3rem;
  background-color: black;
  border: 1px solid rgb(121, 119, 119);
  border-radius: 10px;
  text-align: center;
}
.button.equal {
  width: 47%;
  color: orangered;
}
#ac {
  color: orangered;
}
#div {
  color: rgb(10, 245, 174);
}
.button:hover {
  color: orangered;
  box-shadow: 0.3rem 0.2rem 0.2rem orangered;
}
.row-1,
.row-2,
.row-3,
.row-4,
.row-5 {
  align-items: center;
  margin: auto;
  margin-top: 10px;
  color: white;
  width: 90%;
  height: auto;
  display: flex;
  justify-content: space-between;
  font-size: 35px;
}

.input,
output {
  min-width: 280px;
  width: 100%;
  margin: auto 0;
}
.input {
  color: white;
  font-size: 30px;
}
.output {
  color: white;
  font-size: 25px;
}
</style>
