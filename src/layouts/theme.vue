<template>
  <Countdown />
  <Alert />
</template>

<script>
import Countdown from './components/Countdown.vue'
import Alert from './components/alert.vue'

export default {
  name: 'App',
  components: {
    Countdown,
    Alert
  }
}
</script>
