<template >
    <div class="main">
            <div class="calculator">
                <div class="display">
                        <div class="input">
                            {{input}}
                        </div>
                        <div class="output">
                            {{output}}
                </div>
                </div>
                <div @click="clear()" class="btn">C</div>
                <div @click="cancel()" class="btn">&larr;</div>
                <div @click="enter('%')" class="btn">%</div>
                <div @click="enter('/')" class="btn operator">÷</div>
                <div @click="enter('7')" class="btn">7</div>
                <div @click="enter('8')" class="btn">8</div>
                <div @click="enter('9')" class="btn">9</div>
                <div @click="enter('*')" class="btn operator">x</div>
                <div @click="enter('4')" class="btn">4</div>
                <div @click="enter('5')" class="btn">5</div>
                <div @click="enter('6')" class="btn">6</div>
                <div @click="enter('-')" class="btn operator">-</div>
                <div @click="enter('1')" class="btn">1</div>
                <div @click="enter('2')" class="btn">2</div>
                <div @click="enter('3')" class="btn">3</div>
                <div @click="enter('+')" class="btn operator">+</div>
                <div @click="enter('0')" class="btn zero">0</div>
                <div @click="enter('.')" class="btn">.</div>
                <div @click="equal()" class="btn operator">=</div>
            </div>
    </div>
  
</template>
<script>
export default {
        data() {
            return {
                input: '',
                output:'',
                calculated:false
            }
        },
        methods: {
            clear() {
                this.input=''
                this.output=''
            },
            cancel(){
                //this.input = this.input.slice(0, -1);
                const arr = this.input.split('')
                arr.pop()
                this.input = arr.join('')
            },
            enter(keys){
                if(!this.calculated){
                    this.input +=keys
                }
                else{
                    this.calculated = false
                    this.input=''
                    this.output=''
                    this.input +=keys                
                }
            },
            equal(){
                if(this.input.includes('%')){
                    const arr = this.input.split('')
                    const newArr = []
                    for(let i=0;i<arr.length;i++){
                        if(arr[i]!='%'){
                            newArr.push(arr[i])
                        }
                        else{
                            newArr.push('/100')
                        }
                    }
                    this.input = newArr.join('')
                    console.log(newArr)
                }
                console.log(this.input)
                this.output = eval(this.input)
                this.calculated = true
            }
        },
        
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
                box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
            }
            .calculator {
            margin: 0 auto;
            width: 400px;
            height: 500px;
            font-size: 40px;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-auto-rows: minmax(50px, auto);
         
            }
            .display {
            grid-column: 1 / 5;
            background-color: #333;
            color: white;
            }
            .input{
                min-width: 280px;
                width:100%;
                margin:auto 0;
                color:white;
            }
            .output{
                min-width: 280px;
                width:100%;
                margin:auto 0;
                color:white;
                text-align: left;
            }
            .zero {
            grid-column: 1 / 3;
            }
            .btn {
            background-color: #F2F2F2;
            border: 1px solid #999;
            }
            .operator {
            background-color: orange;
            color: white;
            }
</style>