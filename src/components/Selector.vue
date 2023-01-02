<template>
    <div>
        <select v-model="leccion" name="select">
            <!-- <option value="0" hidden disabled>Elige una lección</option> -->
            <option value="1">Caracteres básicos</option>
            <option value="2">Colores</option>
            <option value="3">Leccion 3</option>
          </select>
    </div>
</template>

<script>
export default {

  data() {
    return {
      leccion: '1'
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
select{
    min-width: 200px;
    height: 50px;
    font-size: 20px;
    padding: 10px;
    text-align: center;
}
</style>