<!--tutorial from freecodeCamp-->
<template>
  <div class="calculator">
    <div class="display">{{current||'0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">/</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="multiply">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="subtract">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked:false,
    }
  },
  methods:{
    //-----------------------------------------
    clear(){
      this.current = '';
    },
  //-----------------------------------------//
    sign(){ //deals with negative sign uses conditional
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
  //-----------------------------------------//
    percent(){
      this.current = `${parseFloat(this.current)/100}`;
    },
  //-----------------------------------------//
    append(number){
      if (this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current =`${this.current}${number}`;
    },
    
    //-----------------------------------------//
    dot(){
      if(this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    //-----------------------------------------
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    //-----------------------------------------//
    divide(){
      this.operator = (a,b) => a/b;
      this.setPrevious();
    },
    //-----------------------------------------
    multiply(){
      this.operator = (a,b) => a*b;
      this.setPrevious();

    },
    //-----------------------------------------
    subtract(){
      this.operator = (a,b) => a-b;
      this.setPrevious();
      
    },
    //-----------------------------------------//
    add(){
      this.operator = (a,b) => a+b;
      this.setPrevious();
    },
    //-----------------------------------------//
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous), 
        parseFloat(this.current)
      )}`;
      this.previous = null;
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.calculator{
  margin: 0 auto;
  width: 400px;
  height: 500px;
  font-size: 40px;
  display:grid;
  grid-template-columns:repeat(4,1fr) ;
  grid-auto-rows: minmax(50px,auto);
  border-color:#A9A9A9;
  border-style:solid;
  border-radius: 10px;
}

.display{
  grid-column: 1/5;
  background-color: #333;
  color:white;
}

.zero{
  grid-column: 1/3;
}

.btn{
  background-color: #F2F2F2;
  border: 1px splid #999;
  cursor:pointer;
}

.operator {
  background-color: orange;
  color:white;
}
.btn:hover { color: #1E90FF; } 


</style>