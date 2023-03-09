<template>
  <div id="app">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top">M =
                <spa v-text="memory"></spa>
              </span>
              <div id="screen_bottom">
                <!-- v-text is a directive that is used to replace the content of HTML tag with private data -->
                <!-- It will update the content automatically when data is changed. It is called data reactive -->
                <span v-text="inputNumber" id="operand1"></span>
                <span v-text="Operator" id="operator"></span>
                <span v-text="secondNumber" id="operand2"></span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <button v-on:click="button_Clear" type="button" class="btn btn-warning">MC</button>
          </td>
          <td>
            <button v-on:click="button_Read" type="button" class="btn btn-warning">MR</button>
          </td>
          <td>
            <button v-on:click="button_Minus" type="button" class="btn btn-warning">M-</button>
          </td>
          <td>
            <button v-on:click="button_Add" type="button" class="btn btn-warning">M+</button>
          </td>
          <td>
            <button 
            v-on:click="deleteLast"
            type="button" class="btn btn-light">
            <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
          </button>
        </td>
      </tr>
      <tr>
        <td>
          <button
          v-on:click="showNumber(7)"
          type="button" class="btn btn-light">7</button>
        </td>
        <td>
          <button
          v-on:click="showNumber(8)"
          type="button" class="btn btn-light">8</button>
        </td>
        <td>
          <button
          v-on:click="showNumber(9)"
          type="button" class="btn btn-light">9</button>
        </td>
        <td>
          <button v-on:click="setOperator(`÷`)" type="button" class="btn btn-secondary">÷</button>
        </td>
        <td>
          <button
          v-on:click="switchSign()"
          type="button" class="btn btn-light">+/-</button>
        </td>
      </tr>
      <tr>
        <td>
          <button
          v-on:click="showNumber(4)"
          type="button" class="btn btn-light">4</button>
        </td>
        <td>
          <button
          v-on:click="showNumber(5)"
          type="button" class="btn btn-light">5</button>
        </td>
        <td>
          <button 
          v-on:click="showNumber(6)"
          type="button" class="btn btn-light">6</button>
        </td>
        <td>
          <button v-on:click="setOperator(`x`)" type="button" class="btn btn-secondary">x</button>
        </td>
        <td>
          <button v-on:click="setOperator(`-`)" type="button" class="btn btn-secondary">-</button>
        </td>
      </tr>
      <tr>
        <td>
          <button
          v-on:click="showNumber(1)"
          type="button"
          class="btn btn-light"
          >
          1
        </button>
      </td>
      <td>
        <button 
        v-on:click="showNumber(2)"
        type="button" class="btn btn-light">2</button>
      </td>
      <td>
        <button 
        v-on:click="showNumber(3)"
        type="button" class="btn btn-light">3</button>
      </td>
      <td rowspan="2">
        <button v-on:click="setOperator(`+`)" type="button" class="btn btn-secondary long-btn">+</button>
      </td>
      <td rowspan="2">
        <button v-on:click="getResult()" type="button" class="btn btn-primary long-btn">=</button>
      </td>
    </tr>
    <tr>
      <td>
        <button
        v-on:click="clear()"
        type="button" class="btn btn-danger">C</button>
      </td>
      <td>
        <button 
        v-on:click="showNumber(0)"
        type="button" class="btn btn-light">0</button>
      </td>
      <td>
        <button v-on:click="isFraction=true" type="button" class="btn btn-light">.</button>
      </td>
    </tr>
  </table>
</div>
<div class="alert alert-danger" id="message_panel" role="alert">
  something wrong here
</div>
</div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  data() {
    return {
      // This is the private data section which can be used inside this component
      inputNumber: 0,
      tmp:null,
      isFraction:false,
      Operator:"",
      secondNumber:"",
      memory:0
      
    };
  },
  methods: {
    button_Read(){
      if(this.Operator==""){
        
        this.inputNumber=this.memory;
        
        
        
      }else{
        this.secondNumber=this.memory;
      }
    },
    button_Clear(){
      this.memory=0
    },
    button_Add(){
      if(this.Operator==""){
        
        this.memory+=this.inputNumber;
        
      }else{
        this.memory+=this.secondNumber;
      }
    },
    button_Minus(){
      if(this.Operator==""){
        
        this.memory-=this.inputNumber;
        
      }else{
        this.memory-=this.secondNumber;
      }
    },
    getResult(){
      if(this.Operator=="+"){
        this.inputNumber=this.inputNumber+this.secondNumber
      }else if(this.Operator=="-"){
        this.inputNumber=this.inputNumber-this.secondNumber
        
      }else if(this.Operator=="x"){
        this.inputNumber=this.inputNumber*this.secondNumber
        
      }else if(this.Operator=="÷"){
        this.inputNumber=this.inputNumber/this.secondNumber
        
      }
      this.Operator="";
      this.secondNumber=""
    },
    clear(){
      this.inputNumber=0;
      this.Operator="";
      this.isFraction=false
      this.secondNumber="";
    },
    switchSign(){
      if(this.Operator==""){
        this.inputNumber=this.inputNumber*-1;
        
      }else{
        this.secondNumber= this.secondNumber*-1;
      }
    }
    ,
    
    deleteLast(){
      if(this.Operator==""){
        if(!isNaN(Number(`${this.inputNumber}`.slice(0, -1)))){
          this.inputNumber=Number(`${this.inputNumber}`.slice(0, -1));
          
        }
        
      }else{
        if(!isNaN(Number(`${this.secondNumber}`.slice(0, -1)))){
          this.secondNumber=Number(`${this.secondNumber}`.slice(0, -1));
          
        }
      }
    },
    setOperator(operator){
      this.Operator=operator;
      
    }
    ,
    showNumber(number) {
      if(this.Operator==""){
        if(!this.isFraction){
          // console.log(Number(`${this.inputNumber}${number}`));
          this.inputNumber = Number(`${this.inputNumber}${number}`);
          
        }else{
          
          
          // console.log(`${this.inputNumber}${number/10}`);
          if(!isNaN(Number(`${this.inputNumber}${number/10}`))){
            this.inputNumber =Number(`${this.inputNumber}${number/10}`);
          }else{
            this.inputNumber = Number(`${this.inputNumber}${number}`);
          }
          this.isFraction=false
        }
      }else{
        if(this.secondNumber==""){
          this.secondNumber=0;
        }
        
        if(!this.isFraction){
          // console.log(Number(`${this.inputNumber}${number}`));
          this.secondNumber = Number(`${this.secondNumber}${number}`);
          
        }else{
          
          
          // console.log(`${this.inputNumber}${number/10}`);
          if(!isNaN(Number(`${this.secondNumber}${number/10}`))){
            this.secondNumber =Number(`${this.secondNumber}${number/10}`);
          }else{
            this.secondNumber = Number(`${this.secondNumber}${number}`);
          }
          this.isFraction=false
        }
      }
      // Assign number when user click to the inputNumber data
      // To access private data from methods, use (this.)
      
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  margin-top: 10em;
  width: 300px;
  border: 1px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 100%;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
#operator {
  background-color: rosybrown;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}
/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}
</style>