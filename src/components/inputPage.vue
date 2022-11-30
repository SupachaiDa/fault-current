<template>
  <div>
    <div class="result"> <!-- Show result -->
      <div v-if="this.showResult === true">
        <div v-if="this.showYINV === false">
          <button v-on:click="this.showYINV = true">Show Z (Y Inverse)</button>
        </div>
        <div v-if="this.showYINV === true" >
          <button v-on:click="this.showYINV = false">Hide Z (Y Inverse)</button>
        </div>
      <div v-if="this.showYINV === true">
         <h5>Y Inverse Positive</h5>
      <div v-for="(n, x) in parseInt(this.totalBus)" :key="x">
         <h5>{{ this.yInversePositive[x] }},</h5>
      </div>
       <h5>---------------------------------------------------------</h5>
      <h5>Y Inverse Negative</h5>
      <div v-for="(n, x) in parseInt(this.totalBus)" :key="x">
         <h5>{{ this.yInverseNegative[x] }},</h5>
      </div>
       <h5>---------------------------------------------------------</h5>
       <h5>Y Inverse Zero</h5>
      <div v-for="(n, x) in parseInt(this.totalBus)" :key="x">
         <h5>{{ this.yInverseZero[x] }},</h5>
      </div>
      <h5>---------------------------------------------------------</h5>
      </div>
      <h5>I(fault 3 Phase) = {{this.faultCurrentThreePhase}} pu</h5>
      <h5> = {{this.faultCurrentThreePhase*this.iBase}} kA</h5>
      <div v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <div v-if="x+1 != parseInt(this.selectedValue+1)">
          <h5>At Bus : {{ this.selectedValue + 1 }} - {{x + 1}} = {{this.currentinEachBus[x]}} pu</h5>
       </div>
      </div>
      <h5>---------------------------------------------------------</h5>
      <h5>I(fault SigleLine to Ground) = {{this.faultCurrentSingleLinetoGround}} pu</h5>
      <h5> = {{this.faultCurrentSingleLinetoGround*this.iBase}} kA</h5>
       <h5>---------------------------------------------------------</h5>
      <h5>I(fault DoubleLine) = {{this.faultCurrentDoubleLine}} pu</h5>
      <h5> = {{this.faultCurrentDoubleLine*this.iBase}} kA</h5>
       <h5>---------------------------------------------------------</h5>
      <h5>I(fault DoubleLine to Ground) = {{this.faultCurrentDoubleLinetoGround}} pu</h5>
      <h5> = {{this.faultCurrentDoubleLinetoGround*this.iBase}} kA</h5>
       <h5>---------------------------------------------------------</h5>
    </div>
    </div>
    <!-- Enter the nuber of bus that the user want to calculate (INT Input) -->
    <h5>Number of Bus (maximum 30 buses)</h5>
    <input type="Int" v-model="totalBusInput" />
     <!-- Enter Base Value -->
    <h5>S(Base) MVA</h5>
    <input type="Float" v-model="this.sBase"/>
    <h5>V(Base) kV</h5>
    <input type="Float" v-model="this.vBase"/>
    <h5>I(Base) kV</h5>
    <input type="Float" v-model="this.iBase"/>
    <!-- ****************************************************** -->
    <!-- After enter the number of bus the user has to press submit button to show calculating results -->
    <button v-on:click="this.selected_to_show = true"><h5>submit</h5></button>
    <h5>-- Fault At Bus --</h5>
     <select v-model="this.selectedValue">
         <option v-for="(n, x) in parseInt(this.totalBus)" :key="x" :value="x">{{x + 1}}</option>
     </select>
    <div v-if="this.selected_to_show === true && this.totalBus <= 30">
       <!-- Recieving Positive Impedance between Bus -->
      <h5>Enter the Impedance (Positive) between each bus</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <div v-for="(n, y) in x + 1" :key="y">
          <div v-if="x != y">
            <h5>Bus {{ x + 1 }}-{{ y + 1 }}</h5>
            <input
              type="Float"
              v-model="this.allBusPositive[parseInt(x)][parseInt(y)]"
            />
          </div>
        </div>
      </div>
       <!-- ****************************************************** -->
       <!-- Recieving Positive Impedance for Generator -->
      <div class="genBus" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>Gen Bus 0-{{ x + 1 }}</h5>
        <input type="Float" v-model="this.genBusPositive[x]" />
          <h5>Ground</h5>
             <input
              type="Float"
              v-model="this.ground1[x]"
            />
      </div>
      <!-- ****************************************************** -->
      <!-- Showing Y Bus result (Positive) -->
      <h5>****** Y BUS Positive ******</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>{{ this.yMetrixPositive[x] }}</h5>
        <h5>,</h5>
      </div>
      <h5>*******************************************</h5>
      <!-- ******************///////////************************* -->
      <!-- ******************///////////************************* -->
          <!-- Recieving Negative Impedance between Bus -->
      <h5>Enter the Impedance (Negative) between each bus</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <div v-for="(n, y) in x + 1" :key="y">
          <div v-if="x != y">
            <h5>Bus {{ x + 1 }}-{{ y + 1 }}</h5>
            <input
              type="Float"
              v-model="this.allBusNegative[parseInt(x)][parseInt(y)]"
            />
          </div>
        </div>
      </div>
       <!-- ****************************************************** -->
       <!-- Recieving Negative Impedance for Generator -->
      <div class="genBus" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>Gen Bus 0-{{ x + 1 }}</h5>
        <input type="Float" v-model="this.genBusNegative[x]" />
          <h5>Ground</h5>
             <input
              type="Float"
              v-model="this.ground2[x]"
            />
      </div>
      <!-- ****************************************************** -->
      <!-- Showing Y Bus result (Negative) -->
      <h5>****** Y BUS Negative ******</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>{{ this.yMetrixNegative[x] }}</h5>
        <h5>,</h5>
      </div>
      <h5>*******************************************</h5>
      <!-- ******************///////////************************* -->
      <!-- ******************///////////************************* -->
        <!-- Recieving Zero Impedance between Bus -->
      <h5>Enter the Impedance (Zero) between each bus</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <div v-for="(n, y) in x + 1" :key="y">
          <div v-if="x != y">
            <h5>Bus {{ x + 1 }}-{{ y + 1 }}</h5>
            <input
              type="Float"
              v-model="this.allBusZero[parseInt(x)][parseInt(y)]"
            />
             <div class="input-group mb-3">
         <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01">1</label>
          </div>
         <select v-model="this.allBusZeroSelected[parseInt(x)][parseInt(y)]" class="custom-select" id="inputGroupSelect01">
             <option selected>Choose...</option>
             <option value="cable">Cable</option>
             <option value="transformerYY">Transformer(Wye-Wye)</option>
             <option value="transformerDD">Transformer(Delta-Delta)</option>
             <option value="transformerYYGround">Transformer(Wye-WyeGround)</option>
             <option value="transformerYGroundYGround">Transformer(WyeGround-WyeGround)</option>
             <option value="transformerYroundD">Transformer(WyeGround-Delta)</option>
             <option value="transformerDY">Transformer(Delta-Wye)</option>
         </select>
        </div>
          </div>
        </div>
      </div>
       <!-- ****************************************************** -->
       <!-- Recieving Zero Impedance for Generator -->
      <div class="genBus" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>Gen Bus 0-{{ x + 1 }}</h5>
        <input type="Float" v-model="this.genBusZero[x]" />
          <h5>Ground</h5>
             <input
              type="Float"
              v-model="this.ground0[x]"
            />
      </div>
      <!-- ****************************************************** -->
      <!-- Showing Y Bus result (Zero) -->
      <h5>****** Y BUS Zero ******</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>{{ this.yMetrixZero[x] }}</h5>
        <h5>,</h5>
      </div>
      <h5>*******************************************</h5>
    </div>
    <!-- ****************************************************** -->
  </div>
   <button @click="show" v-on:click="this.showResult = true">Calculate</button>
</template>
<script>

const math = require('../../node_modules/mathjs/lib/browser/math')


export default {
  name: 'ImgTools',
  methods: {
  },
  mounted() {} /* eslint-disable */,
  data() {
    return {
      totalBusInput: 0,
      selected_to_show: false,
      showResult: false,
      showYINV: false,
      selectedValue: 0,
      busPositive: [],
      genBusPositive: [],
      busNegative: [],
      genBusNegative: [],
      busZero: [],
      genBusZero: [],
      sBase:1,
      vBase:1,
      iBase:1,
      selected1: [],
      selected2: [],
      selected0: [],
      ground1: [],
      ground2: [],
      ground0: [],
      yInversePositive: [],
      yInverseNegative: [],
      yInverseZero: [],
    };
  },
  methods: {
    show() {
      this.yInversePositive = math.inv(this.yMetrixPositive)
      this.yInverseNegative = math.inv(this.yMetrixNegative)
      this.yInverseZero = math.inv(this.yMetrixZero)
    }
  },
  computed: {
    totalBus: {
      get() {
        if(parseInt(this.totalBusInput) > 0) {
          return this.totalBusInput
        } else {
          return 0
        }
      }
    },
    zBase: {
      get() {
        let zBase = parseFloat((math.pow(this.vBase,2))/this.sBase)
        return zBase;
      },
    },
    allBusPositive: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.busPositive.push(newArray);
        }
        return this.busPositive;
      },
    },
    allBusPositiveSelected: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.selected1.push(newArray);
        }
        return this.selected1;
      },
    },
    yMetrixPositive: {
      get() {
        var newArray1 = [0];
        newArray1 = [];

        for (let i = 0; i < this.totalBus; i++) {
          var newArray2 = [0];
          newArray2 = [];
          for (let j = 0; j < this.totalBus; j++) {
            if (i > j) {
              var a = parseFloat(parseFloat(this.allBusPositive[i][j]))
              if (parseFloat(a) === parseFloat(0)) {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / a).toFixed(4));
              }
            } else if (i < j) {
              var b = parseFloat(parseFloat(this.allBusPositive[j][i]))
              if (parseFloat(b) === parseFloat(0)) {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / b).toFixed(4));
              }
            } else if (i === j) {
              var c = parseFloat(0).toFixed(4);
              newArray2.push(c);
            }
          }
          newArray1.push(newArray2);
        }
        // Case i = j
        var d = 0;
        for (let i = 0; i < newArray1.length; i++) {
          for (let j = 0; j < newArray1.length; j++) {
            d = parseFloat(newArray1[i][j]) + d;
          }
          newArray1[i][i] = -parseFloat(
            d + parseFloat(this.busGenPositive[i])
          ).toFixed(4);
          d = 0;
        }
        return newArray1;
      },
    },
    busGenPositive: {
      get() {
        var arrayA = [0];
        arrayA = [];
        for (let i = 0; i <= this.totalBus; i++) {
          let a = this.genBusPositive[i];
          if (parseFloat(a) === parseFloat(0)) {
            arrayA.push(parseFloat(0).toFixed(4));
          } else {
            arrayA.push(parseFloat(this.zBase / this.genBusPositive[i]).toFixed(4));
          }
        }
        return arrayA;
      },
    },
    allBusNegative: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.busNegative.push(newArray);
        }
        return this.busNegative;
      },
    },
    allBusNegativeSelected: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.selected2.push(newArray);
        }
        return this.selected2; //kuy mark
      },
    },
    yMetrixNegative: {
      get() {
        var newArray1 = [0];
        newArray1 = [];

        for (let i = 0; i < this.totalBus; i++) {
          var newArray2 = [0];
          newArray2 = [];
          for (let j = 0; j < this.totalBus; j++) {
            if (i > j) {
              var a = parseFloat(parseFloat(this.allBusNegative[i][j]))
              if (parseFloat(a) === parseFloat(0)) {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / a).toFixed(2));
              }
            } else if (i < j) {
              var b = parseFloat(parseFloat(this.allBusNegative[j][i]))
              if (parseFloat(b) === parseFloat(0)) {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / b).toFixed(4));
              }
            } else if (i === j) {
              var c = parseFloat(0).toFixed(4);
              newArray2.push(c);
            }
          }
          newArray1.push(newArray2);
        }
        // Case i = j
        var d = 0;
        for (let i = 0; i < newArray1.length; i++) {
          for (let j = 0; j < newArray1.length; j++) {
            d = parseFloat(newArray1[i][j]) + d;
          }
          newArray1[i][i] = -parseFloat(
            d + parseFloat(this.busGenNegative[i])
          ).toFixed(4);
          d = 0;
        }
        return newArray1;
      },
    },
    busGenNegative: {
      get() {
        var arrayA = [0];
        arrayA = [];
        for (let i = 0; i <= this.totalBus; i++) {
          let a = this.genBusNegative[i];
          if (parseFloat(a) === parseFloat(0)) {
            arrayA.push(parseFloat(0).toFixed(4));
          } else {
            arrayA.push(parseFloat(this.zBase / this.genBusNegative[i]).toFixed(4));
          }
        }
        return arrayA;
      },
    },
    allBusZero: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.busZero.push(newArray);
        }
        return this.busZero;
      },
    },
     allBusZeroSelected: {
      get() {
        for (let i = 0; i < this.totalBus; i++) {
          var newArray = [0];
          newArray = [];
          for (let j = 0; j <= i; j++) {
            newArray.push(j);
          }
          this.selected0.push(newArray)
        }
        return this.selected0;
      },
    },
    yMetrixZero: {
      get() {
        var newArray1 = [0];
        newArray1 = [];

        for (let i = 0; i < this.totalBus; i++) {
          var newArray2 = [0];
          newArray2 = [];
          for (let j = 0; j < this.totalBus; j++) {
            if (i > j) {
              var a = parseFloat(parseFloat(this.allBusZero[i][j]))
              if (parseFloat(a) === parseFloat(0) || this.allBusZeroSelected[i][j] === 'transformerDD' || this.allBusZeroSelected[i][j] === 'transformerYroundD' || this.allBusZeroSelected[i][j] === 'transformerDY' || this.allBusZeroSelected[i][j] === 'transformerYYGround' || this.allBusZeroSelected[i][j] === 'transformerYY') {
                newArray2.push(parseFloat(0));
              } else {
                  newArray2.push(parseFloat(this.zBase / a).toFixed(4));
              }
            } else if (i < j) {
              var b = parseFloat(parseFloat(this.allBusZero[j][i]))
              if (parseFloat(b) === parseFloat(0) || this.allBusZeroSelected[j][i] === 'transformerDD' || this.allBusZeroSelected[j][i] === 'transformerYroundD' || this.allBusZeroSelected[j][i] === 'transformerDY' || this.allBusZeroSelected[j][i] === 'transformerYYGround' || this.allBusZeroSelected[j][i] === 'transformerYY') {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / b).toFixed(4));
              }
            } else if (i === j) {
              var c = parseFloat(0).toFixed(4);
              newArray2.push(c);
            }
          }
          newArray1.push(newArray2);
        }
        // Case i = j
        var d = 0;
        for (let i = 0; i < newArray1.length; i++) {
          for (let j = 0; j < newArray1.length; j++) {
            d = parseFloat(newArray1[i][j]) + d;
          }
          newArray1[i][i] = -parseFloat(
            d + parseFloat(this.busGenZero[i])
          ).toFixed(4);
          d = 0;
        }
        return newArray1;
      },
    },
    busGenZero: {
      get() {
        var arrayA = [0];
        arrayA = [];
        for (let i = 0; i <= this.totalBus; i++) {
          let a = this.genBusZero[i];
          if (parseFloat(a) === parseFloat(0)) {
            arrayA.push(parseFloat(0).toFixed(4));
          } else {
            arrayA.push(parseFloat(this.zBase / (this.genBusZero[i] + this.ground0[i]*3/this.zBase)).toFixed(4));
          }
        }
        return arrayA;
      },
    },
    faultCurrentThreePhase: {
      get() {
        let i = parseInt(this.selectedValue)
        let fault = 1/this.yInversePositive[i][i]
        return parseFloat(fault).toFixed(4)
      }
    },
    faultCurrentSingleLinetoGround: {
      get() {
        let i = parseInt(this.selectedValue)
        let fault = 1/(this.yInversePositive[i][i] + this.yInverseNegative[i][i] + this.yInverseZero[i][i])
        return parseFloat(fault).toFixed(4)
      }
    },
    faultCurrentDoubleLine: {
      get() {
        let i = parseInt(this.selectedValue)
        let fault = 1/(this.yInversePositive[i][i] + this.yInverseNegative[i][i])
        return parseFloat(fault).toFixed(4)
      }
    },
    faultCurrentDoubleLinetoGround: {
      get() {
        let i = parseInt(this.selectedValue)
        let fault = 1/(this.yInversePositive[i][i] + (this.yInverseNegative[i][i]*this.yInverseZero[i][i])/(parseFloat(this.yInverseNegative[i][i]+this.yInverseZero[i][i])))
        return parseFloat(fault).toFixed(4)
      }
    },
    currentinEachBus: {
      get() {
        var newArray = [0]
        newArray = []
        for(let i = 0; i < this.totalBus; i++) {
          var x = (1 -this.faultCurrentThreePhase*this.yInversePositive[i][this.selectedValue])/this.allBusPositive[i][this.selectedValue]
          if (x === Infinity) {
          newArray.push(0)
          } else if(this.allBusPositive[i].length < parseInt(this.selectedValue + 1)) {
             x = (1 -this.faultCurrentThreePhase*this.yInversePositive[i][this.selectedValue])/this.allBusPositive[this.selectedValue][i]
             newArray.push(parseFloat(x).toFixed(2))
          } else {
            newArray.push(parseFloat(x).toFixed(2))
          }
        }
        return newArray
      }
    }
  },
};
</script>
<style>
.input {
  display: flex;
}
.genBus {
  display: flex;
}
.result {
    text-align: center;
}
</style>
