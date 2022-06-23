<template>

  <section class="src-components-nav-bar-comp">

      <div id="navigator">

        <button id="reset" @click="restart()">{{restartBtn}}</button>
        <span id="message">{{message}}</span>
        
        <button id="easy" :class="{selected : !isHard}" @click="setEasy()">easy</button>
        <button id="hard" :class="{selected :  isHard}" @click="setHard()">hard</button>

      </div>
      
      <ContainerComp
        :squares="squares"
        :pickedColor="pickedColor" 
        @restartBtn="restartBtn=$event" 
        @message="message=$event"
        @win="toggleHeader(true)"
       />

  </section>

</template>

<script>

import ContainerComp from './ContainerComp.vue'
  
  export default  {
    name: 'src-components-nav-bar-comp',
    props: [],
    components: {
      ContainerComp
    },
    mounted () {
      this.init()
    },
    data () {
      return {
        colorCount: 6,
        isHard: true,
        colors: [],
        squares: [],
        pickedColor:'',
        restartBtn: 'New Colors',
        message: ''
      }
    },
    methods: {
      init(){
        this.setColors()
        for(let i = 0; i< this.colorCount; i++){
          this.squares.push({style:{ backgroundColor: this.colors[i] }})
        }
      },
      setColors(){
        this.colors = this.createNewColors(this.colorCount);
        this.pickedColor = this.colors[this.pickColor()];
        this.$emit('pickedColor', this.pickedColor)
      },
      createNewColors(numbers){
        let arr = [];
        for (var i = 0; i < numbers; i++) 
          arr.push(this.createRandomStringColor());
        return arr;  
      },
      createRandomStringColor(){
        let newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")" ;
        return newColor;
      },
      randomInt(){
        return Math.floor(Math.random() * 256);
      },
      pickColor(){
        let quantity;
        if (this.isHard) {
          quantity = 6;
        } else {
          quantity = 3;
        }
        return Math.floor(Math.random() * quantity );
      },
      
      restart(){
        this.message = ''
        this.restartBtn= 'New Colors'
        /* document.querySelector('#header').style.backgroundColor = 'steelblue' */ 
        this.toggleHeader(false)
        this.setColors()
        for(let i = 0; i< this.colorCount; i++){
          this.squares[i].style= { backgroundColor: this.colors[i] };
        }
      },
      setEasy(){    
        if (this.isHard) {
          this.isHard = false;
          this.colorCount = 3
          for (let i = 0; i < this.colorCount; i++) {
            let auxSquare = this.squares[(i+3)]
            auxSquare.style= {...auxSquare.style, display: 'none' };
          }
          this.restart();
        }
      },
      setHard(){
        if (!this.isHard) {
          this.isHard = true;
          this.colorCount = 6;
          for (let i = 0; i < this.colorCount; i++) {
            let auxSquare = this.squares[i]
            auxSquare.style= { ...auxSquare.style, display: 'block' };
          }        
          this.restart();  
        }
      },
      toggleHeader(cond){
        this.$emit('toggleHeader', cond)
      }

    },
    computed: {

    }
}
  
</script>

<style scoped lang="css">

  #navigator {
    background: #ffffff;
    height: 29px;
    text-align: center;
    margin: -1;
    margin-top: -31px;
  }

  #message {
    color: black;
    display: inline-block;
    width: 20%;
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

  .selected {
    background-color: steelblue;
    color: white;
  }

</style>
