<template>
    <div>
        <select v-model="leccion" name="select">
            <option value="0" hidden disabled>Elige una lección</option>
            <option value="1">Leccion 1</option>
            <option value="2">Leccion 2</option>
            <option value="3">Leccion 3</option>
          </select>
    </div>
</template>

<script>
export default {

  data() {
    return {
      leccion: '0'
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

</style>