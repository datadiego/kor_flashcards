<template>
    <div>
        <select v-model="leccion" name="select">
            <option value="value1" selected>Leccion 1</option>
            <option value="value2">Leccion 2</option>
            <option value="value3">Leccion 3</option>
          </select>
    </div>
</template>

<script>
export default {

  data() {
    return {
      leccion: 'value1'
    }
  },
    methods: {
        cargarLeccion(){
            console.log(this.leccion)
        }
    },
  mounted() {
      console.log(this.leccion)
    },
    watch:{
        leccion(anteriorLeccion, nuevaLeccion){
            if(anteriorLeccion !== nuevaLeccion){
                this.cargarLeccion()
            }
        }
    }
}
</script>

<style>

</style>