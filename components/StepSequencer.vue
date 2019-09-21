<template>
  <div class="step-sequencer">
    <bar v-for="i in 16"/>
  </div>
</template>

<script>
  import Bar from '~/components/Bar.vue'
  export default {
    components: {
      Bar
    }
  }
</script>
