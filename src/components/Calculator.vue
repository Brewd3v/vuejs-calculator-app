<template>
  <div class="p-3 calc-container">

    <!-- calc res -->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{calcValue || 0}}
    </div>

    <!-- calc btns -->
    <div class="row g-0">
      <div class="col-3" v-for="element in calcElements" :key="element">
        <div 
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{'bg-vue-green':['C','*','/','-','+','%','='].includes(element)}"
          @click="action(element)"
        >
          {{element}}
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props:{
    msg: String
  },
  data(){
    return{
      calcValue: '',
      prevCalcValue: '',
      calcElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null,
    }
  },
  methods: {
    action(n){

      //append value if nan
      if(!isNaN(n) || n === '.'){
        this.calcValue += n + ''; 
      }

      //clear vals
      if(n === 'C'){
        this.calcValue = ''
      }

      //%
      if(n === '%'){
        this.calcValue = this.calcValue/100 + '';
      }

      //
      if(['/', '*', '-', '+'].includes(n)){
        this.operator = n
        this.prevCalcValue = this.calcValue
        this.calcValue = '';
      }

      //=
      if(n === '='){
        this.calcValue = eval(
          this.prevCalcValue + this.operator + this.calcValue
        );

        this.prevCalcValue = '';
        this.operator = null;
      }


    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

body{
  background: #31475e;
}

.text-right{
  text-align: right;
}

.calc-container{
  max-width: 400px;
  margin: 50px auto;
  background: #234;
}

.bg-vue-dark{
  background: #31475e;
}

.hover-class{
  transition: .3s;
}

.hover-class:hover{
  cursor: pointer;
  background: #3D5875;
}

.bg-vue-green{
  background: #3fb984;
}

</style>
