<template>
    <div>
        <select v-model="tipo_de_ronda" name="selectPregunta">
            <option value="aleatorio">Aleatorio</option>
            <option value="hangul_español">Hangul > Español</option>
            <option value="hangul_coreano">Hangul > Coreano</option>
            <option value="coreano_español">Coreano > Español</option>
            <option value="coreano_hangul">Coreano > Hangul</option>
            <option value="español_hangul">Español > Hangul</option>
            <option value="español_coreano">Español > Coreano</option>
            
          </select>
    </div>
</template>

<script>
export default {

  data() {
    return {
      tipo_de_ronda: 'aleatorio',
    }
  },
    watch:{
        tipo_de_ronda(nuevoTipo, anteriorTipo){
            this.$emit('tipo-pregunta-cambiada', nuevoTipo)
        }
    }
}
</script>

<style>

</style>