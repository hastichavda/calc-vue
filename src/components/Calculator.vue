<template >
  <div class="main">
      <div class="calculator">
            <div class="display">{{ current || '0'}}</div>
            <div v-for="num in num1" class="btn">
              <cal-button :val="num" @append="append" ></cal-button>
            </div>
            <div class="btn" @click="percentage">%</div>
            <div class="btn" @click="back">&larr;</div>
            <div class="btn" @click="sub">-</div>
            <div class="btn" @click="add">+</div>
            <div class="btn" @click="divide">÷</div>
            <div class="btn" @click="mul">×</div>
            <div class="btn zero" @click="equal">=</div>
            <div class="btn" @click="clear">C</div>
            <div class="btn" @click="dot">.</div>
    </div>
  </div>
</template>
<script>
    import calcButton from './calcButton'
    export default {
      components: {
        'cal-button': calcButton
      },
      data() {
        return {
            current: '',
            displayValue:'',
            previous: null,
            operator: null,
            operatorClick: false,
            num1: [ 9 , 8 , 7 , 6 , 5 , 4 , 3 , 2 , 1 , 0 ],
            result: null
        }
      },
      methods: {
          clear() {
            this.current = '';
            this.displayValue='';
            this.result='';
          },
          percentage() {
            this.current = `${parseFloat(this.current) / 100}`
          },
          back() {
            const arr = this.current.split('')
            arr.pop()
            this.current = arr.join('')
          },
          append(number) {
            if(this.operatorClick){
              this.current = '';
              this.operatorClick = false;
            }
            this.current = `${this.current}${number}`;
            this.appendDisplay(number);
          },
          appendDisplay(number)
          {
            this.displayValue = this.displayValue + number;
          },
          dot(){
            if(this.current.indexOf('.') === -1){
              this.append('.');
              this.displayValue('.');
            }
          },
          divide() {
            this.operator = (a,b) => b/a;
            this.setPrev();
            this.appendDisplay('/');
          },
          mul() {
            this.operator = (a,b) => a*b;
            this.setPrev();
             this.appendDisplay('*');
          },
          sub() {
            this.operator = (a,b) => b-a;
            this.setPrev();
             this.appendDisplay('-');
          },
          add() {
            this.operator = (a,b) => a+b;
            this.setPrev();
             this.appendDisplay('+');
          },
          equal() {
            this.current = this.operator(
              parseFloat(this.current),
              parseFloat(this.previous)
            );
            this.previous = null;
          },
          setPrev() {
            this.previous = this.current;
            this.operatorClick = true;
          }
      }
    }
</script>
<style scoped>

  .main{
    background-image: url("1.jpg");
    width:50%;
    height:auto;
    background-color: rgb(201, 42, 42);
    margin:0 auto;           
    border-radius: 10px;
    grid-column:  1 / 5;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  }
  .calculator {
  margin: 0 auto;
  width: 400px;
  height: 500px;
  font-size: 40px;
  display: grid;
  border: 1px solid black;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);

  }
  .display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
  }
 
  .zero {
  grid-column: 1 / 3;
  }
  .btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
  padding: 0 0 0 0;
  }
  .btn:hover{
    background-color:grey;
  }
  .operator {
  background-color: orange;
  color: white;
  border: 1px solid #999;
  }
</style>