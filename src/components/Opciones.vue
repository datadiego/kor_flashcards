<template>
    <div>
        <ul>
            <li
            v-if="tipo_ronda == 'caracter_significado'"
            v-for="opcion in opciones_ronda"
            :key="opcion.id"
            >{{opcion.significado}}</li>
            
            <li
            v-if="tipo_ronda == 'significado_caracter'"
            v-for="opcion in opciones_ronda"
            :key="opcion.id"
            >{{opcion.caracter}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props:{
        opciones_ronda:{
            type: Array,
            required: true
        },
        tipo_ronda:{
            type: String,
            required: true
        }

    }
}
</script>

<style>

</style>