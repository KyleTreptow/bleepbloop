<template>
  <div v-if="synth" class="synth--temp">
    <b>Name:</b> {{ name }}
    <div class="#">
      {{ synth }}
    </div>
    <div class="#">
      <button @click="playNote('C4')">Play Note</button>
    </div>
  </div>
</template>

<script>
import Tone from 'tone';
export default {
  props: ['name'],
  data: function(){
    return {
      message: 'Temp Synth Component',
      synth: false,
      config: {},
      voices: 1
    }
  },
  created: function(){
    // on created
    this.synth = new Tone.MonoSynth().toMaster();
  },
  mounted: function(){
    // on mounted
  },
  computed: {
    // computed values here
  },
  methods: {
    playNote: function(note){
      this.synth.triggerAttackRelease(note, '16n');
    }
  }
}
</script>

<style lang="sass">
.synth--temp
  border: dotted 1px #ddd
  padding: 30px
</style>
