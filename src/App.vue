<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'
import HomeView from './views/HomeView.vue';

const greeting = ref('Hello from parent')
const childMsg = ref('No child msg yet')

const msg = ref('codice from parent')

</script>



<template>
  <header>
    <HelloWorld  @response="(msg) => childMsg = msg"/>
      
    <HomeView :msg="greeting" @response="(msg) => childMsg = msg" />
    <p>{{ childMsg }}</p>

    <HomeView>Messaggio per slot: {{ msg }}</HomeView>

  </header>

  <RouterView />
</template>

<style scoped>
</style>
