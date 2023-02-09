<script setup>
import TheWelcome from '../components/TheWelcome.vue'

  const props = defineProps({
      msg: String
  })

  const emit = defineEmits(['response'])

  emit('response', 'hello from child')

</script>

<template>
  <h1>Part used for props and emits. Another child in app parent</h1>
  <h2>messaggio props: {{ msg || 'No props passed yet' }}</h2>

  <slot>Fallback content</slot>
</template>

<style>
h1 {
  color: green;
}
</style>
