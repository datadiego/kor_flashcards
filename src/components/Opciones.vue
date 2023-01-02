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
    margin: 0;
    margin-bottom: 10px;
}
li{
    display:inline-block;
    padding: 10px;
    margin: 10px;
    border: 6px solid rgb(0, 69, 78);
    border-radius: 12px;
    background-color: aquamarine;
    list-style: none;
    width: 200px;
    text-align: center;
    font-size: 20px;
}
li:hover{
    background-color: lightblue;
}
li:active{
    background-color: lightgreen;
}

@media screen and (max-width: 600px) {
    li{
        width: 100px;
        margin: 5px;
    }
}
</style>