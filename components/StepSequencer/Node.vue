<template>
  <span
  class="seq__bar"
  v-on:click="activate"
  v-bind:class="{ active: active }"
  >
    BAR
  </span>
</template>

<script>
export default {
  data: function() {
    return {
      octave: '4',
      active: false,
    }
  },
  methods: {
    activate: function(){
      this.active = !this.active
    }
  }
}
</script>
