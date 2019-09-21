<template>
  <div class="container">
    <div>
      <section class="####">
        <aside class="####">
          <!-- Aside -->
        </aside>
        <main class="####">

          <step-sequencer />
          <!-- <piano /> -->
        </main>
      </section>
    </div>
  </div>
</template>

<script>
  import Piano from '~/components/Piano.vue'
  import StepSequencer from '~/components/StepSequencer.vue'
  export default {
    components: {
      Piano,
      StepSequencer
    }
  }
</script>
