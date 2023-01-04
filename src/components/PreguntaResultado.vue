<template>
        <div v-if="estado_respuesta=='esperando'">
            <h2 v-if="tipo_ronda_actual=='hangul_coreano'" id="pregunta_actual">{{ pregunta_actual.caracter }}</h2>
            <h2 v-if="tipo_ronda_actual=='hangul_español'" id="pregunta_actual">{{ pregunta_actual.caracter }}</h2>
            <h2 v-if="tipo_ronda_actual=='coreano_español'" id="pregunta_actual">{{ pregunta_actual.pronunciacion }}</h2>
            <h2 v-if="tipo_ronda_actual=='coreano_hangul'" id="pregunta_actual">{{ pregunta_actual.pronunciacion }}</h2>
            <h2 v-if="tipo_ronda_actual=='español_coreano'" id="pregunta_actual">{{ pregunta_actual.significado }}</h2>
            <h2 v-if="tipo_ronda_actual=='español_hangul'" id="pregunta_actual">{{ pregunta_actual.significado }}</h2>
                               
        </div>
        <div v-else-if="estado_respuesta=='correcto'">
            <h2 v-if="numero_ronda>1" @click="getPregunta" id="respuesta_correcta" >{{mensaje}} </h2>
            <p v-else @click="getPregunta" id="respuesta_correcta">{{mensaje}}<br/>(Pulsame para ir a la siguiente pregunta)</p>
        </div>
        <div v-else-if="estado_respuesta=='incorrecto'">
            <h2 v-if="numero_ronda>1" @click="getPregunta" id="respuesta_incorrecta" >{{mensaje}} </h2>
            <p v-else @click="getPregunta" id="respuesta_incorrecta">{{mensaje}}<br/>(Pulsame para ir a la siguiente pregunta)</p>
        </div>
    
</template>

<script>
export default {
    name: "PreguntaResultado",
    props: {
        estado_respuesta: String,
        mensaje: String,
        numero_ronda: Number,
        tipo_ronda_actual: String,
        pregunta_actual: Object
    },

}
</script>

<style>

</style>