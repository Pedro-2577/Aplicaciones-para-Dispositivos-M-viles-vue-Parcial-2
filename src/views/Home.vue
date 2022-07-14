<template>
  <div class="home">
    <h2>Armamento disponible</h2>
     <ListaHome/>
  </div>
</template>

<script>
import ListaHome from '../components/Lista.vue'

export default {
  name: 'IndexHome',
  components: {
    ListaHome
  }
}
</script>