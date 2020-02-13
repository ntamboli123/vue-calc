<template>
 <div class="Calculator">
    <div class="display">{{current || 0}}</div>
        <div class = "btn" @click="clear">C</div>
        <div class = "btn" @click="sign">+/-</div>
        <div class = "btn" @click="percent">%</div>
        <div @click ="division" class = "btn operator">/</div>
        <div @click="append('7')" class = "btn">7</div>
        <div @click="append('8')" class = "btn">8</div>
        <div @click="append('9')" class = "btn">9</div>
        <div @click ="multiply" class = "btn operator">x</div>
        <div @click="append('4')" class = "btn">4</div>
        <div @click="append('5')" class = "btn">5</div>
        <div @click="append('6')" class = "btn">6</div>
        <div @click ="substract" class = "btn operator">-</div>
        <div @click="append('1')" class = "btn">1</div>
        <div @click="append('2')" class = "btn">2</div>
        <div @click="append('3')" class = "btn">3</div>
        <div @click ="add" class = "btn operator">+</div>
        <div @click="append('0')" class = "btn zero">0</div>
        <div @click="dot" class = "btn">.</div>
        <div @click="equals" class = "btn operator">=</div>
 </div>
</template>
<script>
export default {
    data()  {
          return{
              previous: null,
              current: '0',
              operator: '',
              operatorclicked: false
          }
    },
    methods:{
        
        setPrevious()
        {
            this.previous = this.current;
            this.operatorclicked = true;
        },
        clear()
        {
              this.current= '';
        },
        sign(){
          this.current = this.current.charAt(0) === '-' ?
          this.current.slice(1) : `-${this.current}`;
        },
        percent()
          {
            this.current= `${parseFloat(this.current)/100}`
          },
        append(number)
        {
          if(this.operatorclicked)
          {
            this.current = '',
            this.operatorclicked = false;
          }
          this.current = `${this.current}${number}`;

        },
        dot() {
            if(this.current.indexOf('.')===-1)
            {
              this.append('.')

            }
        },
        division()
        {
            this.operator = (a,b) => a / b;
            this.setPrevious()
            //this.operatorclicked = true;
        },
        multiply()
        {
            this.operator = (a,b) => a * b;
            this.setPrevious()
        },
        substract()
        {
            this.operator = (a,b) => a - b;
            this.setPrevious();
            //this.operatorclicked = true;
        },
        add()
        {
            this.operator = (a,b) => a+b;
            this.setPrevious()
        },
        equals()
        {
          //this.operatorclicked = true;
          this.current =`${this.operator(parseFloat(this.previous),parseFloat(this.current))}`;
          this.previous = null;
          //console.log("The current value is  " +this.current);
          //console.log("The old value is  " +this.previous);
        } 
    }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.Calculator{
    width: 400px;
    margin: 0 auto;
    font-size: 20px;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px,auto);

}
.display{
      text-align: center;
      grid-column: 1 / 5;
      background-color: #333;
      color: white
}
.zero{
      text-align: center;
      grid-column: 1 / 3;
}
.btn{
      background-color: #eee;
      border: 1px solid #999;
      text-align: center;
      font-size: 30px;
}
.operator
{
  background-color: orange;
  color: white

}
</style>
