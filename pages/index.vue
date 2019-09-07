<template>
  <div class="container">
    <div>

      <logo />

      <h1 class="title title--main">
        BleepBloop
        <small class="title__sub">
          Browser-Based Synthesizer
        </small>
      </h1>



      <section class="####">
        <aside class="####">

        </aside>
        <main class="####">

        </main>
      </section>



      <piano />

      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <a
            class="button button--main-o"
            href="https://nuxtjs.org/"
            target="_blank"
          >
            Docs
          </a>
        </li>
        <li class="list__item">
          <a
            class="button button--alt-o"
            href="https://github.com/nuxt/nuxt.js"
            target="_blank"
          >
            GitHub
          </a>
        </li>
        <li class="list__item">
          <a
            class="button button--hlt-o"
            href="/buttons/"
            target="_blank"
          >
            Buttons
          </a>
        </li>
      </ul>


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
