<template>
  <div id="app">
    <pm-header></pm-header>
    <router-view></router-view>
    <pm-footer></pm-footer>

  </div> 
</template>

<script>
import PmFooter from '@/components/layouts/footer.vue'
import PmHeader from '@/components/layouts/header.vue'

 export default {
  name: 'app',
  
  
  components:{ PmFooter, PmHeader},

  
}
</script>

<style lang="scss">
 @import './scss/main.scss';

 .encontrados {
   margin-bottom: 25px;
   margin-top: 10px;
 }

 .is-active {
   border: 2px #23d160 solid
 }

</style>
