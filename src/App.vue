<template>
  
  <counter  
    :año="2022"
    :mes="10"
    :dia="11"
    :hora="10"
    :minuto="0"
    :segundo="0"
    :milisegundo="0"
  />
</template>

<script>
import Counter from './components/Counter.vue'


export default {
  name: 'App',
  components: {
    Counter
    
  }
}
</script>

<style>

</style>
