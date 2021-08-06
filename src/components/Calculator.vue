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
      <div class="button" @click="clear">AC</div>
      <div class="button" @click="cancel">&larr;</div>
      <div class="button" @click="enter('%')">%</div>
      <div class="button" @click="enter('/')">/</div>
    </div>
    <div class="row-2">
      <div class="button" @click="enter(7)">7</div>
      <div class="button" @click="enter(8)">8</div>
      <div class="button" @click="enter(9)">9</div>
      <div class="button" @click="enter('*')">*</div>
    </div>
    <div class="row-3">
      <div class="button" @click="enter(4)">4</div>
      <div class="button" @click="enter(5)">5</div>
      <div class="button" @click="enter(6)">6</div>
      <div class="button" @click="enter('-')">-</div>
    </div>
    <div class="row-4">
      <div class="button" @click="enter(1)">1</div>
      <div class="button" @click="enter(2)">2</div>
      <div class="button" @click="enter(3)">3</div>
      <div class="button" @click="enter('+')">+</div>
    </div>
    <div class="row-5">
      <div class="button" @click="enter(0)">0</div>
      <div class="button" @click="enter('.')">.</div>
      <div class="button equal" @click="equal">=</div>
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
  min-width: 350px;
  background-color: black;
  border: 1px solid black;
  border-radius: 10px;
  display: flex;
  font-size: 24px;
  width: 35%;
  height: 30rem;
  margin: auto;
  margin-top: 60px;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}
.display {
  min-width: 300px;
  font-size: 30px;
  width: 90;
  margin: 1rem auto;
  text-align: right;
  height: 120px;
  border: 1px solid grey;
  border-radius: 10px;
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
}
.button:hover,
.button.button.equal:hover {
  color: #f8096d;
  box-shadow: 0.3rem #f8096d;
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
}

.input,
output {
  min-width: 280px;
  width: 100%;
  margin: auto 0;
}
.input {
  color: white;
}
.output {
  color: white;
}
</style>
