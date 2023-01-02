<template>
    <div>
        <ul>
            <li
            v-if="tipo_ronda == 'caracter_significado'"
            v-for="opcion in opciones_ronda"
            :key="opcion.id"
            @click="$emit('select', opcion.significado)"
            >{{opcion.significado}}</li>
            
            <li
            v-if="tipo_ronda == 'significado_caracter'"
            v-for="opcion in opciones_ronda"
            :key="opcion.id"
            @click="$emit('select', opcion.caracter)"
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
ul{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 0;
}
li{
    display:inline-block;
    padding: 10px;
    margin: 10px;
    border: 1px solid black;
    background-color: aquamarine;
    list-style: none;
    width: 200px;
    text-align: center;
}
li:hover{
    background-color: lightblue;
}
li:active{
    background-color: lightgreen;
}
</style>