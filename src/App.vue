<template>
  <div id="app">
    <Header />
    <Navigator @restart="restart($event)"/>
    <div id="container">
      <div v-for="(cuadrado, index) in $store.state.colors" :key="index">
        <Container :color="$store.state.colors[index]" :win="win" @squareSelected="eventClick($event)"/>
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
  props:[],

  data(){
    return{
      win: false
    }
  },
  mounted(){
    this.restart();
    this.$store.state.pickedColor = '';
  },
  methods: {
    eventClick(squareColor){
       //squareColor = this.style.backgroundColor
      if (squareColor === this.$store.state.pickedColor) {
        this.$store.state.restartBtnText = 'Play Again!'
        this.$store.state.messageDisplay = 'You Picked Right';
        this.win = true
        this.setColors(this.$store.state.pickedColor);
        this.$store.state.colorSelection = this.$store.state.pickedColor;
      } else {
        this.$store.state.messageDisplay = "Try Again!";
       // this.style.backgroundColor = "#232323"
        
      }
    },
    setColors(color){
       this.$store.dispatch('setColors', color)
    },

    resetPick(){
      var number;
      if (this.$store.state.isHardSelected) {
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
      this.win = false;
      this.$store.state.colors = this.createNewColors(this.$store.state.colorCount);
      this.$store.state.messageDisplay = "Pick New Colors!";
      this.$store.state.restartBtnText = "New Colors!";
      this.$store.state.pickedColor = this.$store.state.colors[this.resetPick()];
      this.$store.state.colorSelection = "steelblue";
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
