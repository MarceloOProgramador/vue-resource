<template>

  <div id="app">
    
    <search-cep-component></search-cep-component>

  </div>

</template>

<script>
import SearchCepComponent from "./Components/SearchCepComponent"

export default {
  name: 'app',
  data () {
    return {

    }
  },
  components : {

    SearchCepComponent

  }
}
</script>

<style>

</style>
