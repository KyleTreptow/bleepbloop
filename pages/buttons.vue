<template>
  <div class="container">
    <div>
      <h1 class="title title--main">
        Some Button Styles
      </h1>
      <h2 class="title title--sub">
        Regular Buttons
      </h2>
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
          <button class="button button--hlt-o"
            @click="testAlert('This is a test!')"
          >
            Test
          </button>
        </li>
      </ul>
      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <button class="button button--main"
            @click="testAlert('Solid Button Main')"
          >
            Lorem
          </button>
        </li>
        <li class="list__item">
          <button class="button button--alt"
            @click="testAlert('Solid Button Alt')"
          >
            Ipsum
          </button>
        </li>
        <li class="list__item">
          <button class="button button--hlt"
            @click="testAlert('Solid Button Highlight')"
          >
            Dolor
          </button>
        </li>
      </ul>
      <h2 class="title title--sub">
        Small Buttons
      </h2>
      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <button class="button button--main-o button--small"
            @click="testAlert('Small Test #1!')"
          >
            Sit
          </button>
        </li>
        <li class="list__item">
          <button class="button button--alt-o button--small"
            @click="testAlert('Small Test #2!')"
          >
            Amet
          </button>
        </li>
        <li class="list__item">
          <button class="button button--hlt-o button--small"
            @click="testAlert('Small Test #3!')"
          >
            Vis
          </button>
        </li>
      </ul>
      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <button class="button button--main button--small"
            @click="testAlert('Small Test #4!')"
          >
            paulo
          </button>
        </li>
        <li class="list__item">
          <button class="button button--alt button--small"
            @click="testAlert('Small Test #5!')"
          >
            Vivendo
          </button>
        </li>
        <li class="list__item">
          <button class="button button--hlt button--small"
            @click="testAlert('Small Test #6!')"
          >
            Scribentur
          </button>
        </li>
      </ul>
      <h2 class="title title--sub">
        Large Buttons
      </h2>
      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <button class="button button--main-o button--large"
            @click="testAlert('Small Test #7!')"
          >
            Dicta
          </button>
        </li>
        <li class="list__item">
          <button class="button button--alt-o button--large"
            @click="testAlert('Small Test #8!')"
          >
            Oblique Hus
          </button>
        </li>
        <li class="list__item">
          <button class="button button--hlt-o button--large"
            @click="testAlert('Small Test #9!')"
          >
            Vis
          </button>
        </li>
      </ul>
      <!-- Button Row -->
      <ul class="list list--inline">
        <li class="list__item">
          <button class="button button--main button--large"
            @click="testAlert('Small Test #10!')"
          >
            Illud
          </button>
        </li>
        <li class="list__item">
          <button class="button button--alt button--large"
            @click="testAlert('Small Test #11!')"
          >
            Primis
          </button>
        </li>
        <li class="list__item">
          <button class="button button--hlt button--large"
            @click="testAlert('Small Test #12!')"
          >
            Nemei
          </button>
        </li>
      </ul>



    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  methods: {
    testAlert: function(msg){
      alert(msg);
    }
  }
}
</script>
