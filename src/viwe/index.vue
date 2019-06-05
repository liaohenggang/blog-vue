<template>
  <div >
      <v-header></v-header>
      <v-inner></v-inner>
  </div>
</template>

<script>
import header from '../components/header.vue';
export default {
    components:{
        'v-inne':inner,
        'v-header':header,
    }

  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
