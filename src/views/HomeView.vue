<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Badis> </Badis>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Badis from '@/components/Badis.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    Badis
  }

}
</script>
