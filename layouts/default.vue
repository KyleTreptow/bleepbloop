<template>
  <div>
    <div>
      <button @click="playTone('C4')">C4</button>
      <button @click="playTone('Db4')">Db4</button>
      <button @click="playTone('D4')">D4</button>
      <button @click="playTone('Eb4')">Eb4</button>
      <button @click="playTone('E4')">E4</button>
      <button @click="playTone('F4')">F4</button>
      <button @click="playTone('Gb4')">Gb4</button>
      <button @click="playTone('G4')">G4</button>
      <button @click="playTone('Ab4')">Ab4</button>
      <button @click="playTone('A4')">A4</button>
      <button @click="playTone('Bb4')">Bb4</button>
      <button @click="playTone('B4')">B4</button>
    </div>
    <nuxt />
  </div>
</template>

<script>
  import Tone from 'tone';
  export default {
    data: function() {
      return {
        synth: {},
        noise: {}
      }
    },
    beforeMount: function(){
      this.synth = new Tone.Synth().toMaster();
      // this.noise = new Tone.Noise("brown").toMaster().start(0).stop(3);
    },
    mounted: function() {

    },
    methods: {
      playTone: function(note){
        this.synth.triggerAttackRelease(note, '8n');
      },
      playNoise: function(){
        // this.noise.volume.setValueAtTime(-20, 0)
      }
    }
  }
</script>
