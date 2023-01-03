<template>
    <div>
        <select v-model="tipo_de_ronda" name="select">
            <!-- <option value="0" hidden disabled>Elige una lección</option> -->
            <option value="0">Aleatorio</option>
            <option value="1">Hangul > Español</option>
            <option value="2">Hangul > Coreano</option>
            <option value="3">Coreano > Español</option>
            <option value="4">Coreano > Hangul</option>
            <option value="5">Español > Hangul</option>
            <option value="6">Español > Coreano</option>
            
          </select>
    </div>
</template>

<script>
export default {

  data() {
    return {
      tipo_de_ronda: '0',
    }
  },
    watch:{
        leccion(nuevaLeccion, anteriorLeccion){
            this.$emit('leccion-cambiada', nuevaLeccion)
        }
    }
}
</script>

<style>


@media screen and (max-width: 600px) {
  select{
    min-width: 100px;
    font-size: 20px;
    padding: 5px;
    text-align: center;}
}


</style>