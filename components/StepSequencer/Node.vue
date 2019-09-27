<template>
  <span
  class="seq__bar noselect"
  v-on:mousedown="down"
  v-on:mouseup="up"
  v-on:mouseover="hover"
  v-bind:class="{ active: active, highlight: this.step === this.row }"
  >
    {{ this.row }}
  </span>
</template>

<script>
export default {
  props: ['row', 'step'],
  data: function() {
    return {
      octave: '4',
      active: false,
      row: this.row,
      step: this.step,
      notes: [
        {id: "", }
      ]
    }
  },
  methods: {
    down: function(){
      //toggle active state to opposite
      this.active = !this.active
      //set global var to toggle state
      window.active = this.active
      window.mickey = true
    },
    up: function(){ window.mickey = false },
    hover: function(){
      if (window.mickey) {
        this.active = window.active
      }
    }
  }
}
</script>
