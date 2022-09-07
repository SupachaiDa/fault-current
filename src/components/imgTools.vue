<template>
<div class="input">
<h5>Zf</h5><input v-model="rFault" type="Float"><h5>ohm&ensp;</h5>
<h5>S (Base)</h5><input v-model="sBase" type="Float"><h5>MVA&ensp;</h5>
<h5>V (Base)</h5><input v-model="vBase" type="Float"><h5>V&ensp;</h5>
</div>
<h3>Fault Current (3 Phase) &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; I(1) = {{this.threePhaseFaultCurrent}} pu</h3>
<h3>Fault Current (Single line to ground) I(1) = {{this.singleLineFaultCurrent}} pu&ensp;=&ensp;I(2)&ensp;=&ensp;I(0)</h3>
<h3>Fault Current (Line to line)&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; I(1) = {{this.linetoLineFaultCurrent}}</h3>
<h3>Fault Current (Double line to ground) I(1) = {{this.doubleLineFaultCurrent}}</h3>
    <div class="container">
  <div class="row">
    <div class="col-sm">
      <h5>Bus 0</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="0" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
    Fault
  </label>
</div>
    </div>
    <div class="col-sm">
      <div class="box">
        <div v-if="selected[0] === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected[0] === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected[0] === 'transformer'">
          <img v-bind:src="imgTransformer" alt="">
        </div>
      </div>
    </div>
     <div class="col-sm">
      <h5>Bus 1</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="1"  class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2">
  <label class="form-check-label" for="flexRadioDefault2">
    Fault
  </label>
</div>
    </div>
    <div class="col-sm">
      <div class="box">
           <div v-if="selected[1] === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected[1] === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected[1] === 'transformer'">
          <img v-bind:src="imgTransformer" alt="">
        </div>
      </div>
    </div>
     <div class="col-sm">
      <h5>Bus 2</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="2" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault3">
  <label class="form-check-label" for="flexRadioDefault3">
    Fault
  </label>
</div>
    </div>
    <div class="col-sm">
      <div class="box">
         <div v-if="selected[2] === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected[2] === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected[2] === 'transformer'">
          <img v-bind:src="imgTransformer" alt="">
        </div>
      </div>
    </div>
     <div class="col-sm">
      <h5>Bus 3</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="3" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault4">
  <label class="form-check-label" for="flexRadioDefault4">
   Fault
  </label>
</div>
    </div>
    <div class="col-sm">
      <div class="box">
         <div v-if="selected[3] === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected[3] === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected[3] === 'transformer'">
          <img v-bind:src="imgTransformer" alt="">
        </div>
      </div>
    </div>
     <div class="col-sm">
      <h5>Bus 4</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="4" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault5">
  <label class="form-check-label" for="flexRadioDefault5">
    Fault
  </label>
</div>
    </div>
    <div class="col-sm">
      <div class="box">
         <div v-if="selected[4] === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected[4] === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected[4] === 'transformer'">
          <img v-bind:src="imgTransformer" alt="">
        </div>
      </div>
    </div>
     <div class="col-sm">
      <h5>Bus 5</h5>
      <div class="form-check">
  <input v-model="selectedRadio" value="5" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
    Fault
  </label>
</div>
    </div>
  </div>
  <div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">1</label>
  </div>
  <select v-model="selected[0]" class="custom-select" id="inputGroupSelect01">
    <option selected>Choose...</option>
    <option value="generator">Generator</option>
    <option value="cable">Cable</option>
    <option value="transformer">Transformer</option>
  </select>
</div>
<div class="input">
<h5>X0</h5><input v-model="x[0][0]" type="Float">
  <h5>X1</h5><input v-model="x[0][1]" type="Float">
  <h5>X2</h5><input v-model="x[0][2]" type="Float">
</div>
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">2</label>
  </div>
  <select v-model="selected[1]" class="custom-select" id="inputGroupSelect01">
    <option selected>Choose...</option>
    <option value="generator">Generator</option>
    <option value="cable">Cable</option>
    <option value="transformer">Transformer</option>
  </select>
</div>
<div class="input">
 <h5>X0</h5><input v-model="x[1][0]" type="Float">
  <h5>X1</h5><input v-model="x[1][1]" type="Float">
  <h5>X2</h5><input v-model="x[1][2]" type="Float">
</div>
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">3</label>
  </div>
  <select v-model="selected[2]" class="custom-select" id="inputGroupSelect01">
    <option selected>Choose...</option>
    <option value="generator">Generator</option>
    <option value="cable">Cable</option>
    <option value="transformer">Transformer</option>
  </select>
</div>
<div class="input">
  <h5>X0</h5><input v-model="x[2][0]" type="Float">
  <h5>X1</h5><input v-model="x[2][1]" type="Float">
  <h5>X2</h5><input v-model="x[2][2]" type="Float">
</div>
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">4</label>
  </div>
  <select v-model="selected[3]" class="custom-select" id="inputGroupSelect01">
    <option selected>Choose...</option>
    <option value="generator">Generator</option>
    <option value="cable">Cable</option>
    <option value="transformer">Transformer</option>
  </select>
</div>
<div class="input">
  <h5>X0</h5><input v-model="x[3][0]" type="Float">
  <h5>X1</h5><input v-model="x[3][1]" type="Float">
  <h5>X2</h5><input v-model="x[3][2]" type="Float">
</div>
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <label class="input-group-text" for="inputGroupSelect01">5</label>
  </div>
  <select v-model="selected[4]" class="custom-select" id="inputGroupSelect01">
    <option selected>Choose...</option>
    <option value="generator">Generator</option>
    <option value="cable">Cable</option>
    <option value="transformer">Transformer</option>
  </select>
</div>
<div class="input">
  <h5>X0</h5><input v-model="x[4][0]" type="Float">
  <h5>X1</h5><input v-model="x[4][1]" type="Float">
  <h5>X2</h5><input v-model="x[4][2]" type="Float">
</div>
</div>
</template>
<script>
const generatorUrl = require('../assets/img_generator.jpeg')
const cableUrl = require('../assets/img_cable.jpeg')
const transformerUrl = require('../assets/img_transformer.jpeg')
const math = require('../../node_modules/mathjs/lib/browser/math')

export default {
  name: 'ImgTools',
  mounted() {
  }, /* eslint-disable */
  data() {
    return {
      selected: [null, null, null, null, null],
      imgGen: generatorUrl,
      imgCable: cableUrl,
      imgTransformer: transformerUrl, 
      x: [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]], 
      rFault: 0,
      selectedRadio: 0,
      sBase: 0,
      vBase: 0
    }
  },
  computed: {
    rFaultPu: {
      get() {
        let v = parseFloat(this.vBase)
        let vv = math.pow(v,2)
        let zBase = math.divide(vv,parseFloat(this.sBase))
        let y = math.divide(parseFloat(this.rFault),zBase)
        return y
      }
    },
    genPosition: {
      get() {
        let genPs = []
        for(let i = 0; i < 5; i++) {
          if (this.selected[i] === 'generator') {
            genPs.push(i)
          }
         }
        return genPs
      }
    },
    largestNum: {
      get() {
        let largestN
        for(let i = 0; i < this.genPosition.length; i ++) {
          if(this.genPosition[i] < this.genPosition[i+1]) {
            largestN = this.genPosition[i+1]
          }
        }
        return parseInt(largestN)
      }
    },
     xTotalZero: {
     get() {
        let xTotal = 0
        let xTotal1 = 0
        let xTotal2 = 0
        if(this.largestNum > this.selectedRadio) { // In case the system has more than two generators that the fault location is being between two of them
        for(let i = 0; i < this.selectedRadio; i++) {
          xTotal1 += parseFloat(this.x[i][0])
        }
         for(let i = this.selectedRadio; i <= this.largestNum; i++) {
          xTotal2 += parseFloat(this.x[i][0])
        }
         xTotal = (parseFloat(xTotal1)*parseFloat(xTotal2))/(parseFloat(xTotal1)+parseFloat(xTotal2)) //sum resistor for each side in serie method, and after that sum both of them in parallel method
         
        }else { // In case the generator is situated before or after fault location
          for(let i = 0; i < this.selectedRadio; i++) {
          xTotal += parseFloat(this.x[i][0])
        }
        }
        return parseFloat(xTotal).toFixed(2)
    }
  },
    xTotalPositive: {
     get() {
        let xTotal = 0
        let xTotal1 = 0
        let xTotal2 = 0
        if(this.largestNum > this.selectedRadio) { // In case the system has more than two generators that the fault location is being between two of them
        for(let i = 0; i < this.selectedRadio; i++) {
          xTotal1 += parseFloat(this.x[i][1])
        }
         for(let i = this.selectedRadio; i <= this.largestNum; i++) {
          xTotal2 += parseFloat(this.x[i][1])
        }
         xTotal = (parseFloat(xTotal1)*parseFloat(xTotal2))/(parseFloat(xTotal1)+parseFloat(xTotal2)) //sum resistor for each side in serie method, and after that sum both of them in parallel method
         
        }else { // In case the generator is situated before or after fault location
          for(let i = 0; i < this.selectedRadio; i++) {
          xTotal += parseFloat(this.x[i][1])
        }
        }
        return parseFloat(xTotal).toFixed(2)
    }
  },
  xTotalNegative: {
     get() {
        let xTotal = 0
        let xTotal1 = 0
        let xTotal2 = 0
        if(this.largestNum > this.selectedRadio) { // In case the system has more than two generators that the fault location is being between two of them
        for(let i = 0; i < this.selectedRadio; i++) {
          xTotal1 += parseFloat(this.x[i][2])
        }
         for(let i = this.selectedRadio; i <= this.largestNum; i++) {
          xTotal2 += parseFloat(this.x[i][2])
        }
         xTotal = (parseFloat(xTotal1)*parseFloat(xTotal2))/(parseFloat(xTotal1)+parseFloat(xTotal2)) //sum resistor for each side in serie method, and after that sum both of them in parallel method
         
        }else { // In case the generator is situated before or after fault location
          for(let i = 0; i < this.selectedRadio; i++) {
          xTotal += parseFloat(this.x[i][2])
        }
        }
        return parseFloat(xTotal).toFixed(2)
    }
  },
  threePhaseFaultCurrent: {
    get() {
      let x = math.complex(parseFloat(this.rFaultPu),parseFloat(this.xTotalPositive))
      let y = math.divide(1,x)
      return `${parseFloat(y.re).toFixed(2)} ${parseFloat(y.im).toFixed(2)}i`
    }
  },
    singleLineFaultCurrent: {
    get() {
      let complex =  parseFloat(this.xTotalZero)+parseFloat(this.xTotalPositive)+parseFloat(this.xTotalNegative)
      let real = parseFloat(this.rFaultPu)*3
      let x = math.complex(real,complex)
      let y = math.divide(1,x)
      return `${parseFloat(y.re).toFixed(2)} ${parseFloat(y.im).toFixed(2)}i`
    }
  },
    linetoLineFaultCurrent: {
    get() {
      let complex = parseFloat(this.xTotalPositive)+parseFloat(this.xTotalNegative)
      let real = parseFloat(this.rFaultPu)
      let x = math.complex(real,complex)
      let y = math.divide(1,x)
      let yNeg = math.subtract(0,y)
      return `${parseFloat(y.re).toFixed(2)} ${parseFloat(y.im).toFixed(2)}i pu ,I(2) = ${parseFloat(yNeg.re).toFixed(2)} ${parseFloat(yNeg.im).toFixed(2)}i pu`
    }
  },
   doubleLineFaultCurrent: {
    get() {
     let r = math.complex(parseFloat(this.rFaultPu)*3,parseFloat(this.xTotalZero))  // R(fault) + X(zero)
     let rNegative = math.complex(0,parseFloat(this.xTotalNegative))
     let rr = math.multiply(r,rNegative)  //  (R(fault) + X(zero)) * X(negative)
     let rrr = math.add(r,rNegative)  // (R(fault) + X(zero)) + X(negative)
     let rparallel = math.divide(rr,rrr)
     let rPositive = math.complex(0,parseFloat(this.xTotalPositive))
     let x = math.add(rPositive,rparallel)
     let y = math.divide(1,x)
     let rSecond = math.divide(r,rrr)
     let iSecond = math.multiply(rSecond,y)
     let z = math.subtract(0,iSecond)
     let rZero = math.divide(rNegative,rrr)
     let iZero = math.multiply(rZero,y)
     let zz = math.subtract(0,iZero)
    return `${parseFloat(y.re).toFixed(2)} ${parseFloat(y.im).toFixed(2)}i pu ,I(2) = ${parseFloat(z.re).toFixed(2)} ${parseFloat(z.im).toFixed(2)}i pu ,I(0) = ${parseFloat(zz.re).toFixed(2)} ${parseFloat(zz.im).toFixed(2)}i pu`
    }
  }
  }
}
</script>
<style>
.box {
  width: 150px;
  height: 150px;
  padding: 10px;
  border: 5px solid gray;
  margin: 0;
  }
  .input {
  display: flex;
  }
</style>
