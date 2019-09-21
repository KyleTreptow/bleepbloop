<template>
  <div class="container">
    <div>
      <logo />
      <piano />
    </div>
  </div>
</template>

<script>

  import Logo from '~/components/Logo.vue'
  import Piano from '~/components/Piano.vue'

  export default {
    components: {
      Logo,
      Piano
    }
  }

</script>
