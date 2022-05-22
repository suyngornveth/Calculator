<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div class="btn" @click="clear">AC</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="time" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorClick: false
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      if (!this.current) {
        this.append('0');
      }
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`

    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if(this.operatorClick){
        this.current = '';
        this.operatorClick = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {

      if (this.current.indexOf('.') === -1) {
        this.current ? this.append('.') : this.append('0.')

      }
    },
    setPrevious(){
      this.previous = this.current,
      this.operatorClick = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
      
    },
    time() {
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
    equal(){
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
  font-size: 22pt;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

div {
  padding-top: 10px;
}

.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #FEFEFE;
  border: 1px solid #999;
}

.operator {
  color: white;
  background-color: orange;
}
</style>
