<template>
    <div>
        <h1>🥬 Kimchi Cards 🥬</h1>
        <Selector @leccion-cambiada="actualizarLeccion" />

        <h2>{{ leccion_actual }}</h2>
        <!-- <Selector/> -->
        <h2>Simbolo</h2>
        <Opciones/>
    </div>
</template>

<script>
import Selector from './Selector.vue'
import Opciones from './Opciones.vue'

export default {
    name: 'Pagina',
    data(){
        return{
            leccion_actual: "1",
            preguntas: null,
            pregunta_actual: null,
        }
    },
    methods:{
        actualizarLeccion(nuevaLeccion){
            this.leccion_actual = nuevaLeccion
            this.getLeccion()
        },
        getLeccion(){
            console.log(this.leccion_actual)
            if(this.leccion_actual == '1'){
                //cargar desde csv
                console.log("Cargando csv", this.leccion_actual)
        }
    }
},
    components: {
        Selector,
        Opciones
    },
    
}
</script>

<style>

</style>