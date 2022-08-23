
<template>
<div class="input">
<h5>Zf</h5><input v-model="xFault" type="h">
</div>
<h3>Fault Current = {{this.faultCurrent}} pu</h3>
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
        <div v-if="selected1 === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected1 === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected1 === 'transformer'">
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
           <div v-if="selected2 === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected2 === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected2 === 'transformer'">
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
         <div v-if="selected3 === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected3 === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected3 === 'transformer'">
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
         <div v-if="selected4 === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected4 === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected4 === 'transformer'">
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
         <div v-if="selected5 === 'generator'">
          <img v-bind:src="imgGen" alt="">
        </div>
        <div v-else-if="selected5 === 'cable'">
          <img v-bind:src="imgCable" alt="">
        </div>
        <div v-else-if="selected5 === 'transformer'">
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
  <select v-model="selected1" class="custom-select" id="inputGroupSelect01">
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
  <select v-model="selected2" class="custom-select" id="inputGroupSelect01">
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
  <select v-model="selected3" class="custom-select" id="inputGroupSelect01">
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
  <select v-model="selected4" class="custom-select" id="inputGroupSelect01">
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
  <select v-model="selected5" class="custom-select" id="inputGroupSelect01">
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
export default {
  name: 'ImgTools',
  mounted() {
  }, /* eslint-disable */
  data() {
    return {
      selected1: null,
      selected2: null,
      selected3: null,
      selected4: null,
      selected5: null,
      imgGen: generatorUrl,
      imgCable: cableUrl,
      imgTransformer: transformerUrl, 
      x: [[0, parseFloat(0), 0], [0, parseFloat(0), 0], [0, parseFloat(0), 0], [0, parseFloat(0), 0], [0, parseFloat(0), 0]], 
      xFault: 0,
        selectedRadio: 0
    }
  },
  computed: {
    xTotal1: {
     get() {
        let xTotal = 0
        for(let i = 0; i < this.selectedRadio; i++) {
          xTotal += parseFloat(this.x[i][1])
        }
        return parseFloat(xTotal).toFixed(2)
    }
  },
  faultCurrent: {
    get() {
      return parseFloat(1/(this.xTotal1+parseFloat(this.xFault))).toFixed(2)
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
