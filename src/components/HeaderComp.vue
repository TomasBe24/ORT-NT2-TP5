<template>

  <section class="src-components-header-comp">

    <div id="header" :style=" win ? {background : pickedColor} : '' ">

      <h1>The Great <br>
        <span id="colorDisplay">{{pickedColor != ''? pickedColor : 'RGB' }} </span>
        <br>
        Guessing Game</h1>

    </div>

    <NavBarComp @pickedColor="pickedColor=$event" @toggleHeader="toggleHeader($event)" />
  
  </section>

</template>

<script>
  import NavBarComp from './NavBarComp.vue'

  export default  {
    name: 'src-components-header-comp',
    props: [],
    components: {
      NavBarComp
    },
    mounted () {

    },
    data () {
      return {
        pickedColor:'',
        win : false,
        color : ''
      }
    },
    methods: {
      toggleHeader(event){
        this.win = event
      }

    },
    computed: {

    }
}

</script>

<style scoped lang="css">
  

  #header {
	transition: all 0.3s;
	background: steelblue;
	text-transform: uppercase;
	text-align: center;
	margin: 0;
	color: white;
  }

  #colorDisplay {
    font-size: 200%;
  }



</style>
