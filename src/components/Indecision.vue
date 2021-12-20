<template>
<img v-if="img" :src="img" alt="bg"> <!-- Si hay imagen (v-if="img")-->
<div class="bg-dark"></div>

<div class="indecision-container">
    <input v-model="question" type="text" placeholder="Hazme una pregunta">
    <p>Recuerda poner un el signo ? al final de la pregunta</p>

    <div v-if="isValidQuestion"> <!-- Si la pregunta es válida-->
        <h2>{{question}}</h2>
        <h1>{{ answer === 'yes' ? 'Si !' : 'No !'}}</h1>
    </div>
</div>
   
</template>

<script>
import { watch } from '@vue/runtime-core'

export default {
    data() {
        return {
            question: null,
            answer: null,
            img: null,
            isValidQuestion: false
        }
    },
    methods: {
       async getAnswer(){
           this.answer = 'Pensando....'
           const {answer, image} = await fetch('https://yesno.wtf/api').then(resp => resp.json())
           
           console.log(answer, image)
           
           this.answer = answer
           // también se podia hacer así
           //this.answer = answer == 'yes' ? ' Si !' : 'No !'
           this.img = image
           
        }
    },
    // Observar
    watch: {
        question(value, oldValue){
            // La pregunta no es válida
            this.isValidQuestion = false
            // Si no incluye el signo ? haz un return
            if(!value.includes('?')) return
            // Si hay un ?
            // La pregunta ya es válida
            this.isValidQuestion = true
            // Realizar petición http
            this.getAnswer()
        }
    }
    
    
}
</script>


<style>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }
</style>
