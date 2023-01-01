<template>
    <div>
        <h1>🥬 Kimchi Cards 🥬</h1>
        <Selector/>
        <h2>Simbolo</h2>
        <Opciones/>
    </div>
</template>

<script>
import Selector from './Selector.vue'
import Opciones from './Opciones.vue'

export default {
    name: 'Pagina',
    components: {
        Selector,
        Opciones
    }
}
</script>

<style>

</style>