<template>
  <div id="app">
    <Header :color="pickedColor" :colorSelection="colorSelection"/>
    <Navigator :message="messageDisplay" @restart="restart($event)" :restartBtn="restartBtnText" @colorCount="colorCount=$event" @isHardSelected="isHardSelected=$event" />
    <div id="container">
      <div v-for="(cuadrado, index) in colors" :key="index">
        <Container :color="colors[index]" @squareSelected="eventClick($event)"/>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Navigator from './components/Navigator.vue'
import Container from './components/Container.vue'

export default {
  name: 'App',
  components: {
    Header,
    Navigator,
    Container
  },
  props:['isHardSelected', 'colorCount'],

  data(){
    return{
      colors: [],
      pickedColor: '',
      messageDisplay: '',
      colorSelection: '',
      restartBtnText: '',


    }
  },
  mounted(){
    this.restart();
    this.pickedColor = '';
  },
  methods: {
    eventClick(squareColor){
       squareColor = this.style.backgroundColor
      if (squareColor === this.pickedColor) {
        this.restartBtnText = "Play Again!"
        this.messageDisplay = "You Picked Right!"
        this.setColors(this.pickedColor);
        this.colorSelection = this.pickedColor
      } else {
        this.messageDisplay = "Try Again!"
        this.style.backgroundColor = "#232323"
        this.messageDisplay.style.color = "#000000";
      }
    },
    setColors(color){
      for (let i = 0; i < this.colors.length; i++) {
        this.colors[i] = color;
      }
    },

    resetPick(){
      var number;
      if (this.isHardSelected) {
        number = 6
      } else{
        number = 3
      }
      return Math.floor(Math.random() * number)
    },

    randomInt(){
      return Math.floor(Math.random() * 256)
    },  

    createRgb(){
      var newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() +  ")"
      return newColor
    },

    createNewColors(numbers){
      var arr = [];
        for (var i = 0; i < numbers; i++) {
          arr.push(this.createRgb());
        }
        return arr;
    },

    restart(){
      this.colors = this.createNewColors(this.colorCount)
      this.messageDisplay = ""
      this.restartBtnText = "NEW COLORS!"
      this.pickedColor = this.colors[this.resetPick()]
      this.colorSelection = "steelblue"
    }
  }
}
</script>

<style>
#app {
  background: #232323;
	margin: 0;
	font-family: "Montserrat", "Avenir";
}
body {
	background: #232323;
	margin: 0;
	font-family: "Montserrat", "Avenir";
}
#container {
	margin: 20px auto;
	max-width: 600px;
}

</style>
