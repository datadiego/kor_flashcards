<template>
    <div class="page-cointainer">
        <h1>🥬 Kimchi Cards 🥬</h1>
        <Selector @leccion-cambiada="actualizarLeccion" />
        <div v-if="leccion_cargada">
            <Puntos :aciertos="aciertos" :fallos="fallos" />
            <h2 v-if="tipo_ronda_actual=='caracter_significado'" id="pregunta_actual">{{ pregunta_actual.caracter }}</h2>
            <h2 v-else id="pregunta_actual">{{ pregunta_actual.significado }}</h2>
        </div>
        <div v-if="!leccion_cargada">
            <h2>Selecciona una lección para empezar</h2>
            
        </div>
        <Opciones @select="checkAnswer($event)" :opciones_ronda="preguntas" :tipo_ronda="tipo_ronda_actual"/>
    </div>
</template>

<script>
import Selector from './Selector.vue'
import Opciones from './Opciones.vue'
import Puntos from './Puntos.vue'

import leccion1 from '../assets/coreano1.csv'
import leccion2 from '../assets/coreano2.csv'

export default {
    name: 'Pagina',
    data(){
        return{
            leccion_actual: "1",
            preguntas: [],
            pregunta_actual: null,
            leccion_cargada: false,
            tipos_ronda: ['caracter_significado','significado_caracter'],
            tipo_ronda_actual: null,
            aciertos: 0,
            fallos: 0,
            flag_ronda_terminada: false,
            
        }
    },
    methods:{
        actualizarLeccion(nuevaLeccion){
            this.leccion_actual = nuevaLeccion
            this.getLeccion()
        },
        getLeccion(){
            if(this.leccion_actual == '1'){
                this.preguntas = leccion1.slice(0,4)
            }
            else if(this.leccion_actual == '2'){
                this.preguntas = leccion2.slice(0,4)
            }
            else{
                console.log("Cargamos leccion", this.leccion_actual)
            }
            const randint = Math.floor(Math.random() * this.preguntas.length)
            this.pregunta_actual = this.preguntas[randint]
            this.leccion_cargada = true
    },
    checkAnswer(respuesta){
        if(this.flag_ronda_terminada){
            return undefined
        }
        if(this.tipo_ronda_actual == 'caracter_significado'){
            if(respuesta == this.pregunta_actual.significado){
                this.aciertos += 1
            }
            else{
                this.fallos += 1
            }
        }
        else{
            if(respuesta == this.pregunta_actual.caracter){
                this.aciertos += 1
            }
            else{
                this.fallos += 1
            }
        }
        const randint = Math.floor(Math.random() * this.preguntas.length)
        this.pregunta_actual = this.preguntas[randint]
    }
},
    components: {
        Selector,
        Opciones,
        Puntos
    },
    beforeMount(){
        const randint = Math.floor(Math.random() * this.tipos_ronda.length)
        this.tipo_ronda_actual = this.tipos_ronda[randint]
    },
    
}
</script>

<style>
.page-cointainer{
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    width: 100vw;
    background-color: #f5f5f5;
    text-align: center;
}

#pregunta_actual{
    background-color: aquamarine;
    font-size: 50px;
    border-radius: 30px;
    padding: 20px;
}
</style>