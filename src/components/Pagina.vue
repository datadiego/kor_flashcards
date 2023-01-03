<template>
    <div class="page-cointainer">
        <h1 id="kimchichards">🥬 Kimchi Cards 🥬</h1>
        <div class="juego">
            <div v-if="leccion_cargada">
                <Puntos :aciertos="aciertos" :fallos="fallos" />
                <h2 v-if="tipo_ronda_actual=='caracter_significado'" id="pregunta_actual">{{ pregunta_actual.caracter }}</h2>
                <h2 v-else id="pregunta_actual">{{ pregunta_actual.significado }}</h2>
            </div>
            <div v-if="!leccion_cargada">
                <h2>Selecciona una lección para empezar</h2>
            </div>
            <Opciones @select="checkAnswer($event)" :opciones_ronda="preguntas" :tipo_ronda="tipo_ronda_actual"/>
            
            <h2 v-show="flag_ronda_terminada" id="respuesta">{{mensaje}}</h2>
            <button v-show="flag_ronda_terminada" @click="getPregunta">Siguiente</button>
            <Selector @leccion-cambiada="actualizarLeccion" />
        </div>

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
            mensaje: "",
            flag_ronda_terminada: false,
            leccion1: leccion1,
            leccion2: leccion2
            
        }
    },
    methods:{
        actualizarLeccion(nuevaLeccion){
            this.leccion_actual = nuevaLeccion
            this.getPregunta()
        },
        shuffle(array) {
        array.sort(() => Math.random() - 0.5)
            },
        getPregunta(){
            this.flag_ronda_terminada = false
            if(this.leccion_actual == '1'){
                this.shuffle(this.leccion1)
                this.preguntas = this.leccion1.slice(0,4)
                console.log(this.preguntas)
            }
            else if(this.leccion_actual == '2'){
                this.shuffle(this.leccion2)
                this.preguntas = this.leccion2.slice(0,4)
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
            return
        }
        else{
        if(this.tipo_ronda_actual == 'caracter_significado'){
            if(respuesta == this.pregunta_actual.significado){
                this.aciertos += 1
                this.mensaje = `¡Correcto! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
            }
            else{
                this.fallos += 1
                this.mensaje = `Error! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
            }
        }
        else{
            if(respuesta == this.pregunta_actual.caracter){
                this.aciertos += 1
                this.mensaje = `¡Correcto! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
            }
            else{
                this.fallos += 1
                this.mensaje = `Error! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
            }
        }

        this.flag_ronda_terminada = true
    }
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
    mounted(){
        this.actualizarLeccion(this.leccion_actual)
    }
    
}
</script>

<style>
body{
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
    color: #ff00ff;
    margin: 0;
    padding: 0;
}

.page-cointainer{
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    width: 100vw;
    background-color: #ff9cf7;
    text-align: center;
}
#respuesta{
    font-size: 30px;
    margin-top: 0px;
    margin-bottom: 15px;
    color: #212121;
}
#opciones{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    margin-top: 20px;
}
#pregunta_actual{
    background-color: #ff00ff  ;
    color: #212121 ;
    border: 6px solid #a000a0;
    box-shadow: 0px 8px 0px #550044;
    font-size: 50px;
    border-radius: 10px;
    padding: 12px;
    margin: 0px;
    min-width: 100px;
    margin-bottom: 60px;
    
}

button{
    margin: 0;
    background-color: #ff00ff;
    border: 6px solid #a000a0;
    color: #212121;
    box-shadow: 3px 3px 0px #550044;
    font-size: 20px;
    border-radius: 12px;
    padding: 12px;
    min-width: 100px;
}
#kimchicards{
    color: #ffd54f
}
@media screen and (max-width: 600px){
    #pregunta_actual{
        font-size: 60px;
        margin: 20px;
    }
    #respuesta{
        font-size: 20px;
    }
    button{
        font-size: 15px;
    }
    h1, h2{
        margin:10px;
    }
    
}
</style>