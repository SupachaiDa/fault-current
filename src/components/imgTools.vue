
<template>
<div class="input">
<h5>Zf</h5><input v-model="xFault" type="h">
</div>
    <div class="container">
  <div class="row">
    <div class="col-sm">
      <h5>Bus 0</h5>
      <div class="form-check">
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
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
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
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
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
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
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
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
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
  <label class="form-check-label" for="flexRadioDefault1">
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
  <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">
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
  <h5>X0</h5><input v-model="xFirst[0]" type="h">
  <h5>X1</h5><input v-model="xFirst[1]" type="h">
  <h5>X2</h5><input v-model="xFirst[2]" type="h">
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
  <h5>X0</h5><input v-model="xSecond[0]" type="h">
  <h5>X1</h5><input v-model="xSecond[1]" type="h">
  <h5>X2</h5><input v-model="xSecond[2]" type="h">
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
  <h5>X0</h5><input v-model="xThird[0]" type="h">
  <h5>X1</h5><input v-model="xThird[1]" type="h">
  <h5>X2</h5><input v-model="xThird[2]" type="h">
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
  <h5>X0</h5><input v-model="xFourth[0]" type="h">
  <h5>X1</h5><input v-model="xFourth[1]" type="h">
  <h5>X2</h5><input v-model="xFourth[2]" type="h">
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
  <h5>X0</h5><input v-model="xFifth[0]" type="h">
  <h5>X1</h5><input v-model="xFifth[1]" type="h">
  <h5>X2</h5><input v-model="xFifth[2]" type="h">
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
  },
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
      xFirst: [0, 0, 0],
      xSecond: [0, 0, 0],
      xThird: [0, 0, 0],
      xFourth: [0, 0, 0],
      xFifth: [0, 0, 0],
      xFault: 0
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
