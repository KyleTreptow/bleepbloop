<template>
<<<<<<< HEAD
  <div class="container">
    <div>
      <logo />
      <piano />
=======
  <div class="app">
      <header class="app__header">
        App Header
      </header>
      <section class="app__body">
        <aside class="app__aside">
          <p>Instrument Stack...</p>
        </aside>
        <main class="app__main">
          <step-sequencer />
        </main>
      </section>
      <footer class="app__footer">
        Footer Here
      </footer>
>>>>>>> origin/step-sequencer
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
