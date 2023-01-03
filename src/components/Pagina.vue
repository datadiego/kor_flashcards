<template>
    <div class="page-cointainer">
        <h1 id="kimchichards">🥬 Kimchi Cards 🥬</h1>
        <div id="juego">
            <div v-if="leccion_cargada">
                <Puntos :aciertos="aciertos" :fallos="fallos" />
                <div v-if="estado_respuesta=='esperando'">
                    <h2 v-if="tipo_ronda_actual=='caracter_significado'" id="pregunta_actual">{{ pregunta_actual.caracter }}</h2>
                    <h2 v-else id="pregunta_actual">{{ pregunta_actual.significado }}</h2>                    
                </div>
                <div v-else-if="estado_respuesta=='correcto'">
                    <h2 v-if="numero_ronda>1" @click="getPregunta" id="respuesta_correcta" >{{mensaje}} </h2>
                    <p v-else @click="getPregunta" id="respuesta_correcta">{{mensaje}}<br/>(Pulsame para ir a la siguiente pregunta)</p>
                </div>
                <div v-else-if="estado_respuesta=='incorrecto'">
                    <h2 v-if="numero_ronda>1" @click="getPregunta" id="respuesta_incorrecta" >{{mensaje}} </h2>
                    <p v-else @click="getPregunta" id="respuesta_incorrecta">{{mensaje}}<br/>(Pulsame para ir a la siguiente pregunta)</p>
                </div>
            </div>
            <div v-if="!leccion_cargada">
                <h2>Selecciona una lección para empezar</h2>
            </div>
            <OpcionesRespuesta @select="checkAnswer($event)" :opciones_ronda="preguntas" :tipo_ronda="tipo_ronda_actual"/>
        </div>
        <h1>⚙️ Opciones ⚙️</h1>
        <SelectorLeccion @leccion-cambiada="actualizarLeccion" />
        <SelectorTipoPregunta @leccion-cambiada="actualizarLeccion" />

    </div>
</template>

<script>
import SelectorLeccion from './SelectorLeccion.vue'
import SelectorTipoPregunta from './SelectorTipoPregunta.vue'
import OpcionesRespuesta from './OpcionesRespuesta.vue'
import Puntos from './Puntos.vue'

import leccion1 from '../assets/coreano1.csv'
import leccion2 from '../assets/coreano2.csv'
import leccion3 from '../assets/coreano3.csv'
import leccion4 from '../assets/coreano4.csv'
import leccion5 from '../assets/coreano5.csv'

export default {
    name: 'Pagina',
    data(){
        return{
            leccion_actual: "1",
            preguntas: [],
            pregunta_actual: null,
            leccion_cargada: false,
            tipos_ronda: ['aleatorio', 'hangul_español','hangul_coreano','coreano_español', 'coreano_hangul', 'español_hangul', 'español_coreano'],
            tipo_ronda_actual: 'aleatorio',
            aciertos: 0,
            fallos: 0,
            mensaje: "",
            flag_ronda_terminada: false,
            flag_primera_ronda: true,
            estado_respuesta: "esperando",
            numero_ronda: 0,
            leccion1: leccion1,
            leccion2: leccion2,
            leccion3: leccion3,
            leccion4: leccion4,
            leccion5: leccion5,
            lecciones: [leccion1, leccion2, leccion3, leccion4, leccion5],
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
            this.estado_respuesta = "esperando"
            this.numero_ronda += 1

            if(this.numero_ronda === 2){
                this.flag_primera_ronda = false
            }
            this.flag_ronda_terminada = false
            if(this.tipo_ronda_actual == "aleatorio"){
                const randint = Math.floor(Math.random() * this.tipos_ronda.length)
                this.tipo_ronda_actual = this.tipos_ronda[randint]
            }
            else{
                if(this.tipo_ronda_actual == "caracter_significado"){
                    this.tipo_ronda_actual = "significado_caracter"
                }
                else{
                    this.tipo_ronda_actual = "caracter_significado"
                }
            }
            for (let i = 0; i < this.lecciones.length; i++) {
                if(this.leccion_actual == i+1){ 
                    this.shuffle(this.lecciones[i])
                    this.preguntas = this.lecciones[i].slice(0,4)
                }
            }

            const randint = Math.floor(Math.random() * this.preguntas.length)
            this.pregunta_actual = this.preguntas[randint]
            this.leccion_cargada = true
    },
    comprueba_respuesta(respuesta){
        if(respuesta == this.pregunta_actual){
            this.aciertos += 1
            this.estado_respuesta = "correcto"
            this.mensaje = "¡Correcto!"
        }
        else{
            this.fallos += 1
            this.estado_respuesta = "incorrecto"
            this.mensaje = "¡Incorrecto!"
        }
    },
    creaMensaje(){
        if(this.estado_respuesta == "correcto"){
            this.mensaje = `¡Correcto! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
        }
        else{
            this.mensaje = `¡Incorrecto! ${this.pregunta_actual.caracter} significa ${this.pregunta_actual.significado}`
        }
    },
    checkAnswer(respuesta){
        if(!this.flag_ronda_terminada){
            this.comprueba_respuesta(respuesta)
            this.creaMensaje()
            this.flag_ronda_terminada = true
        }
    }
},
    components: {
        SelectorLeccion,
        OpcionesRespuesta,
        SelectorTipoPregunta,
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
    overflow: hidden;
    width: 100%;
    background-color: #ff9cf7;
    text-align: center;
}
#respuesta{
    font-size: 30px;
    margin-top: 0px;
    margin-bottom: 15px;
    color: #212121;
    cursor: pointer;
}
#opciones{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
}
#juego{
    background-color: rgb(255, 255, 141);
    padding: 12px;
    border-radius: 12px;
    box-shadow: 0px 8px 0px #a0a000;
    border: 6px solid #a0a000;
    margin: 0px;
    width: 600px;
    min-height: 46em;
    margin-bottom: 20px
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
    height: 130px;
    display: flex;
    align-items: center;
    justify-content: center;
    
}
#respuesta{
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
    height: 130px;
    display: flex;
    align-items: center;
    justify-content: center;
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
    margin-bottom: 20px;
}
#respuesta_correcta{
    background-color: #81ffa1  ;
    color: #212121 ;
    border: 6px solid #a000a0;
    box-shadow: 0px 8px 0px #550044;
    font-size: 30px;
    border-radius: 10px;
    padding: 12px;
    margin: 20px;
    min-height: 130px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    margin-bottom: 60px;
}
#respuesta_incorrecta{
    background-color: #ff6a6a  ;
    color: #212121 ;
    border: 6px solid #a000a0;
    box-shadow: 0px 8px 0px #550044;
    font-size: 30px;
    border-radius: 10px;
    padding: 12px;
    margin: 20px;
    margin-bottom: 60px;
    min-height: 130px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
}
#kimchicards{
    color: #ffd54f
}
@media screen and (max-width: 600px){

    #pregunta_actual{
        font-size: 40px;
        margin: 20px;
        margin-bottom: 20px;
    }
    #respuesta{
        background-color: #ff00ff  ;
        color: #212121 ;
        border: 6px solid #a000a0;
        box-shadow: 0px 8px 0px #550044;
        font-size: 30px;
        border-radius: 10px;
        padding: 12px;
        margin: 20px;
    }
    #respuesta_correcta{
        margin-bottom: 20px;
    }
    #respuesta_incorrecta{
        margin-bottom: 20px;
    }

    button{
        font-size: 15px;
        margin-bottom: 20px;
    }
    h1, h2{
        margin:10px;
    }
    #juego{
        width: 300px;
        min-height: 310px;
    }
    
    
}
</style>