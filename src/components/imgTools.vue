<template>
  <div>
    <!-- Enter the nuber of bus that the user want to calculate (INT Input) -->
    <h5>Number of Bus (maximum 30 buses)</h5>
    <input type="Int" v-model="totalBus" />
     <!-- Enter Base Value -->
    <h5>S(Base) MVA</h5>
    <input type="Float" v-model="this.sBase"/>
    <h5>V(Base) kV</h5>
    <input type="Float" v-model="this.vBase"/>
    <!-- ****************************************************** -->
    <!-- After enter the number of bus the user has to press submit button to show calculating results -->
    <button v-on:click="this.selected_to_show = true"><h5>submit</h5></button>
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
        <div class="input-group mb-3">
         <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01">1</label>
          </div>
         <select v-model="this.allBusPositiveSelected[parseInt(x)][parseInt(y)]" class="custom-select" id="inputGroupSelect01">
             <option selected>Choose...</option>
             <option value="generator">Generator</option>
             <option value="cable">Cable</option>
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
        <h5>,length of array = {{ this.yMetrixPositive[x].length }}</h5>
      </div>
      <h5>length of array = {{ this.yMetrixPositive.length }}</h5>
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
             <div class="input-group mb-3">
         <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01">1</label>
          </div>
         <select v-model="this.allBusNegativeSelected[parseInt(x)][parseInt(y)]" class="custom-select" id="inputGroupSelect01">
             <option selected>Choose...</option>
             <option value="generator">Generator</option>
             <option value="cable">Cable</option>
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
        <h5>,length of array = {{ this.yMetrixNegative[x].length }}</h5>
      </div>
      <h5>length of array = {{ this.yMetrixNegative.length }}</h5>
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
             <option value="generator">Generator</option>
             <option value="cable">Cable</option>
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
      <!-- Showing Y Bus result (Positive) -->
      <h5>****** Y BUS Zero ******</h5>
      <div class="input" v-for="(n, x) in parseInt(this.totalBus)" :key="x">
        <h5>{{ this.yMetrixZero[x] }}</h5>
        <h5>,length of array = {{ this.yMetrixZero[x].length }}</h5>
      </div>
      <h5>length of array = {{ this.yMetrixZero.length }}</h5>
      <h5>*******************************************</h5>
      <button @click="inverse()"><h5>Calculate Y inverse</h5></button>
      <h5 id="title1"></h5>
      <h5 id="view1"></h5>
      <h5 id="title2"></h5>
      <h5 id="view2"></h5>
      <h5 id="title0"></h5>
      <h5 id="view0"></h5>
    </div>
    <!-- ****************************************************** -->
  </div>
</template>
<script>
const math = require('../../node_modules/mathjs/lib/browser/math')

export default {
  name: 'ImgTools',
  methods: {
    inverse: function () {
      // For Positive
      document.getElementById('title1').innerHTML +=
        'Y BUS (POSITIVE) INVERSED'
      const A = math.inv(this.yMetrixPositive)
      // Setting text in element
      for (let i = 0; i < this.totalBus; i++) {
        for (let j = 0; j < this.totalBus; j++) {
          if (parseInt(j) === 0 && parseInt(i) === 0) {
            document.getElementById('view1').innerHTML +=
              '[' + '&nbsp;&nbsp;&nbsp;' + parseFloat(A[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) !== parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view1').innerHTML +=
              parseFloat(A[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '[' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) === parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view1').innerHTML +=
              parseFloat(A[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '<br/>'
          } else {
            document.getElementById('view1').innerHTML +=
              parseFloat(A[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          }
        }
      }
      // ******************************************************
       // For Negative
      document.getElementById('title2').innerHTML +=
        'Y BUS (NEGATIVE) INVERSED'
      const B = math.inv(this.yMetrixNegative)
      // Setting text in element
      for (let i = 0; i < this.totalBus; i++) {
        for (let j = 0; j < this.totalBus; j++) {
          if (parseInt(j) === 0 && parseInt(i) === 0) {
            document.getElementById('view2').innerHTML +=
              '[' + '&nbsp;&nbsp;&nbsp;' + parseFloat(B[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) !== parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view2').innerHTML +=
              parseFloat(B[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '[' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) === parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view2').innerHTML +=
              parseFloat(B[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '<br/>'
          } else {
            document.getElementById('view2').innerHTML +=
              parseFloat(B[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          }
        }
      }
      // ******************************************************
       // For Zero
      document.getElementById('title0').innerHTML +=
        'Y BUS (ZERO) INVERSED'
      const C = math.inv(this.yMetrixZero)
      // Setting text in element
      for (let i = 0; i < this.totalBus; i++) {
        for (let j = 0; j < this.totalBus; j++) {
          if (parseInt(j) === 0 && parseInt(i) === 0) {
            document.getElementById('view0').innerHTML +=
              '[' + '&nbsp;&nbsp;&nbsp;' + parseFloat(C[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) !== parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view0').innerHTML +=
              parseFloat(C[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '[' + '&nbsp;&nbsp;&nbsp;'
          } else if (
            parseInt(j) === parseInt(this.totalBus - 1) &&
            parseInt(i) === parseInt(this.totalBus - 1)
          ) {
            document.getElementById('view0').innerHTML +=
              parseFloat(C[i][j]).toFixed(4) + '&nbsp;&nbsp;&nbsp;' + ']' + '<br/>'
          } else {
            document.getElementById('view0').innerHTML +=
              parseFloat(C[i][j]).toFixed(4) + ',' + '&nbsp;&nbsp;&nbsp;'
          }
        }
      }
      // ******************************************************
    }
  },
  mounted() {} /* eslint-disable */,
  data() {
    return {
      totalBus: 0,
      selected_to_show: false,
      busPositive: [],
      genBusPositive: [],
      busNegative: [],
      genBusNegative: [],
      busZero: [],
      genBusZero: [],
      sBase:1,
      vBase:1,
      selected1: [],
      selected2: [],
      selected0: [],
      ground1: [],
      ground2: [],
      ground0: [],
    };
  },
  computed: {
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
              if (parseFloat(a) === parseFloat(0)) {
                newArray2.push(parseFloat(0));
              } else {
                newArray2.push(parseFloat(this.zBase / a).toFixed(4));
              }
            } else if (i < j) {
              var b = parseFloat(parseFloat(this.allBusZero[j][i]))
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
            arrayA.push(parseFloat(this.zBase / this.genBusZero[i]).toFixed(4));
          }
        }
        return arrayA;
      },
    },
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
</style>
