<template>
  <div >
      <v-header class="header"></v-header>
      <v-inner></v-inner>
  </div>
</template>

<script>
import header from '../components/header.vue';
import inner from '../components/inner.vue';
export default {
    components:{
        'v-inner':inner,
        'v-header':header,
    }

  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header{
    height: 100px;

}

</style>
