<template>
  <span
  class="seq__bar noselect"
  v-on:mousedown="down"
  v-on:mouseup="up"
  v-on:mouseover="hover"
  v-bind:class="{ active: active, highlight: this.step === this.row }"
  >
  {{ row }}  {{ notes[col-1]["note"] }}
  </span>
</template>

<script>
export default {
  props: ['col', 'row', 'step', 'synth'],
  data: function() {
    return {
      octave: '4',
      active: false,
      notes: [
        { note: 'C', color: 'white' },
        { note: 'Db', color: 'black' },
        { note: 'D', color: 'white' },
        { note: 'Eb', color: 'black' },
        { note: 'E', color: 'white' },
        { note: 'F', color: 'white' },
        { note: 'Gb', color: 'black' },
        { note: 'G', color: 'white' },
        { note: 'Ab', color: 'black' },
        { note: 'A', color: 'white' },
        { note: 'Bb', color: 'black' },
        { note: 'B', color: 'white' }
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
    },
    playNote: function(){
      this.synth.triggerAttackRelease(this.notes[this.col-1]["note"]+this.octave, '16n');
    }
  },
  watch: {
    step: function(newStep) { // watch it
      if (newStep === this.row && this.active){
        this.playNote()
      }
    }
  }
}
</script>
