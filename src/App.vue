<template>
  <div id="app">
    <div class="progressBar">
      <div class="barContainer">
        <span class="bar" :style="barWidth"></span>
      </div>
      <div class="etape active">1</div>
      <div class="etape" :class="{active : step2}">2</div>
      <div class="etape" :class="{active : step3}">3</div>
      <div class="etape" :class="{active : step4}">4</div>
    </div>
    <div class="boutonContainer">
      <button @click="prevStep" class="bouton prev">
        Prev
      </button>
      <button @click="nextStep" class="bouton next">
        Next
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'ProgressBar',
  data() {
    return {
      index: 1,
      step2: false,
      step3: false,
      step4: false,
      width: 5
    }
  },
  methods: {
    nextStep() {
      if (this.index < 4) {
        this.index++
        this.width += 30
      }
      if(this.index == 2) {
        this.step2 = true
      }
      else if(this.index == 3) {
        this.step3 = true
      }
      else if (this.index == 4) {
        this.step4 = true
      }
    },
    prevStep() {
      if(this.index == 2) {
        this.step2 = false
      }
      else if(this.index == 3) {
        this.step3 = false
      }
      else if (this.index == 4) {
        this.step4 = false
      }
      if (this.index > 1) {
        this.index--
        this.width -= 30
      }
    }
  },
   computed: {
    barWidth () {
      return {
        width: `${this.width}%`,
      }
    }
   }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  #app {
    font-family: Avenir, Helvetica, Arial;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: #f6f7fb;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .progressBar {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 350px;
  }
  .barContainer {
    position: absolute;
    width: 100%;
    height: 4px;
    background-color: #e0e0e0;
    z-index: 1;
  }
  .bar {
    position: absolute;
    width: 5%;
    height: 100%;
    background-color: #3498db;
    transition: 0.4s ease;
  }
  .etape {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: #fff;
    font-weight: bold;
    color: #999;
    border: 3px solid #e0e0e0;
    transition: 0.4s ease;
    z-index: 2;
  }
  .etape.active {
    border: 3px solid #3498db;
  }
  .bouton {
    width: 90px;
    height: 35px;
    background-color: #3498db;
    color: #fff;
    border-radius: 7px;
    border: none;
    margin-top: 50px;
    margin: 35px 0 0 0;
    outline: none;
    cursor: pointer;
    transition: all 0.1s ease-in-out;
     transform: scale(1);
  }
  .bouton.prev {
    margin-right: 10px;
    background-color: #e0e0e0;
  }
  .bouton:active {
    transform: scale(0.96);
  }
  @media screen and (max-width: 370px) {
    .progressBar {
      width: 280px;
    }
  }
</style>
