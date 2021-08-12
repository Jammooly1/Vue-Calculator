<template>
  <div class="p-3" style="max-width: 500px; margin: 0px auto; background: #234; border-radius: 5px; box-shadow: gray .5px .5px .5px .5px;">
      
      <div class="input-group mt-2 mb-3 input_button">
        <input  type="text" v-model="calculatorValue" class="form-control" placeholder="" aria-label="math equation" aria-describedby="basic-addon2">
        <div class="input-group-append">
            <button @click="buttons('solve')" class="btn bg-vue-green btn-lg text-white" type="button">SOLVE</button>
        </div>
      </div>


        <div class="row no-gutters">
            <div class="col-3" v-for="n in calculatorElements" :key="n">
                <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
                :class="{'bg-vue-green': ['C','*','/','-','+','%','=', 'DEL'].includes(n)}"
                @click="buttons(n)">
                    {{n}}
                </div>
            </div>
            <div v-if="err">
                <p class="error">{{err}}</p>
            </div>
            
        </div>
  </div>
</template>

<script> 
import { ref } from '@vue/reactivity'
export default {
    name: 'Calculator',
    setup() {
         const calculatorValue = ref('')
         const calculatorElements = ['C','*','/','DEL','7','8','9','-','4','5','6','+','1','2','3','%','0','.', '=']
         const err = ref('')
         let solved = false

        const buttons = (n) => {
            err.value = ''
            if(n === 'DEL') {
                console.log('DEL', calculatorValue.value)
                calculatorValue.value = calculatorValue.value.toString().slice(0,-1)
            }
            else if(n === 'C') {
                calculatorValue.value = ''
            }
            else if(n === '=' || n === 'solve'){
                try {
                    calculatorValue.value = eval(calculatorValue.value)
                    solved = true
                } catch(error) {
                    console.log(error.message)
                    err.value = 'BAD INPUT'
                }
            } else {
                if(!solved && n !== 'DEL') {
                    calculatorValue.value += n
                } else {
                    if(['*', '/', '-', '+','%'].includes(n)) {
                        calculatorValue.value += n
                    }
                    else if(!isNaN(n) || n === '.') {
                        calculatorValue.value = n
                    }
                    solved = false
                }
            }
        }
         return { calculatorValue, buttons, calculatorElements, err }
    }
}
</script>

<style scoped>
  .input_button {
      text-align: center;   
      max-width: 95%;  
      margin: 0 auto; 
  }
 .bg-vue-dark {
    background: #31475e;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #3D5875;
  }
  .bg-vue-green {
    background: #3fb984;
  }
  .error {
      color: rgb(223, 0, 0);
      font-size: 50px;
      font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
  }
</style>