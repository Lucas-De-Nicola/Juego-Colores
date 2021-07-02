<template>

  <section class="src-components-navigator">
    <div id="navigator">
		  <button id="reset" @click="eventBtnRestart()">{{this.$store.state.restartBtnText}}</button>
		  <span id="message">  {{this.$store.state.messageDisplay}}</span>

	  	<button id="easy" :class="{selected: isEasySelected}" @click="eventBtnEasy()">easy</button>
		  <button id="hard" :class="{selected: isHardSelected}" @click="eventBtnHard()">hard</button>
	  </div>

  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-navigator',
    props: [],
    mounted () {

    },
    data () {
      return {
        
      }
    },
    methods: {
      eventBtnEasy(){
         if(this.$store.state.isHardSelected){
          this.$store.state.isHardSelected = false;
          this.$store.state.isEasySelected = true;
          this.$store.state.colorCount = 3;
          this.$emit('restart', this.$store.state.colorCount)
        }
      },
      eventBtnHard(){
        if(!this.$store.state.isHardSelected){
          this.$store.state.isHardSelected = true;
          this.$store.state.isEasySelected = false;
          this.$store.state.colorCount = 6;
          this.$emit('restart', this.$store.state.colorCount)
        }
      },
      eventBtnRestart(){
        this.$emit('restart', this.$store.state.colorCount)
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-navigator {

  }

  .selected {
	  background-color: steelblue;
	  color: white;
  }

  button {
	  border: none;
	  background-color: white;
	  font-family: "Montserrat", "Avenir";
	  text-transform: uppercase;
	  height: 100%;
	  font-weight: 700;
	  letter-spacing: 1px;
	  color: steelblue;
	  transition: all 0.3s;
	  outline: none;
  }

  button:hover {
	  color: white;
	  background-color: steelblue;  
  }

  #message {
	  
	  display: inline-block;
	  width: 20%;
  }

  #navigator {
	  background: #ffffff;
	  height: 30px;
	  text-align: center;
	  margin: 0;
	  margin-top: -30px;
  }
</style>
