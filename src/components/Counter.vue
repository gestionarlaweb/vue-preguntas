<template>
 <h2>{{customTitle}}</h2>
  <p> {{counter}} <sup>2</sup> = {{squareCounter}}</p>

  <div>
    <button @click="increment">
      +1
    </button>
    <button v-on:click="decrement">
      -1
    </button>
  </div>
    
</template>

<script>
export default {
  props: {
    title : String,
    start: {
      type: Number, 
      default: 100,
      //required: true
      validator(value){
        return value >=0
      }
    }
  },
    data(){
      return { 
        counter: this.start
      }
  },
  methods: {
    getSquareValue(){
      return this.counter * this.counter
    },
    increment(){
      return this.counter++
    },
    decrement(){
      return this.counter--
    }
  },
  computed: {
    squareCounter(){
      return this.counter * this.counter
    },
    customTitle(){
      if (this.title != undefined) {
        return this.title
      } else {
        return 'Counter'
      }
    }
  }
}
</script>

<style>
button{
    background-color: #64B687;
    border-radius: 5px;
    border: 1px solid white;
    color: white;
    cursor: pointer;
    margin: 0 5px;
    padding: 5px 15px;
    transition: 0.3s ease-in-out;
}
button:hover {
    background-color: #5aa67b;
    transition: 0.3s ease-in-out;
}

</style>
