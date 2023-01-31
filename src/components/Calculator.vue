<template>
  <div class="">
    <h1>{{ msg }}</h1>
  </div>

  <div class="container">
    <div class="row">
      <div class="col-md-6 mx-auto py-5">
        <table class="table table-bordered">
          <tbody>
            <tr>
              <td colspan="4" class="output">{{ output || 0 }}</td>
            </tr>
            <tr>
              <td class="fw-bold" @click="clearField">C</td>
              <td class="fw-bold" @click="setNegativeOrPositive">+ / -</td>
              <td @click="calculatePercentage"><i class="fa-solid fa-percent"></i></td>
              <td class="lastColumn" @click="processOutput('division')"><i class="fa-solid fa-divide"></i></td>
            </tr>
            <tr>
              <td @click="getNumber('7')">7</td>
              <td @click="getNumber('8')">8</td>
              <td @click="getNumber('9')">9</td>
              <td class="lastColumn" @click="processOutput('multiply')">x</td>
            </tr>
            <tr>
              <td @click="getNumber('4')">4</td>
              <td @click="getNumber('5')">5</td>
              <td @click="getNumber('6')">6</td>
              <td class="lastColumn" @click="processOutput('sub')">-</td>
            </tr>
            <tr>
              <td @click="getNumber('1')">1</td>
              <td @click="getNumber('2')">2</td>
              <td @click="getNumber('3')">3</td>
              <td class="lastColumn" @click="processOutput('add')">+</td>
            </tr>
            <tr>
              <td colspan="2" @click="getNumber('0')">0</td>
              <td @click="getDot()">.</td>
              <td class="lastColumn" @click="updateOutput">=</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorApp',
  props: {
    msg: String
  },
  data(){
    return{
      output:'',
      previousValue: null,
      operationFired: false,
    }
  },
  methods:{
    clearField(){
      this.output = ''
    },
    setNegativeOrPositive(){
      this.output = this.output[0] === '-' ? this.output.slice(1) : `-${this.output}`;
    },
    calculatePercentage(){
      this.output = parseFloat(this.output)/100;
    },
    getNumber(number){

      if(this.operationFired){
        this.output = '';
        this.operationFired = false;
      }

      this.output =  `${this.output}${number}`;
    },
    getDot(){
      if(this.output.indexOf('.') === -1){
        this.output = this.output+ '.';
      }
    },
    processOutput(string){

      if(string == 'add'){
        this.operation = (a,b) => {
        return parseFloat(a) + parseFloat(b);
      }
      }
      else if(string == 'sub'){
        this.operation = (a,b) => {
          return parseFloat(a) + parseFloat(b);
        }
      }
      else if(string == 'multiply'){
        this.operation = (a,b) => {
          return parseFloat(a) * parseFloat(b);
        }
      }
      else if(string == 'division'){
        this.operation = (a,b) => {
          return parseFloat(a) / parseFloat(b);
        }
      }

      this.previousValue = this.output;
      this.operationFired = true;

    },

    updateOutput(){
      this.output = `${this.operation(this.previousValue, this.output )}`;
      this.previousValue = null;
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} 
.output{
  background-color: #03001C;
  color: #fff;
}
.lastColumn {
  background-color: #DC0000;
  color: #fff;
}
.lastColumn:active{
  background-color: #03001C;
  color: #fff;
}
td{
  background-color: #00425A;
  color: #fff;
}
</style>
