<template>
  <div class="piano">
    <ul class="piano__octave-list">
      <li
        v-for="n in 6"
        class="piano__octave-item"
      >
        <button
          :class="octaveClass(n)"
          @click="changeOctive(n)"
        >
          {{ n }}
        </button>
      </li>
    </ul>
    <div class="piano__roll">
      <button
        v-for="key in keys"
        :class="keyClass(key.color)"
        @click="playTone(key.note + octave)"
      >
        <span class="piano__label">
          {{ key.note + octave}}
        </span>
      </button>
    </div>
  </div>
</template>

<script>

  var log = console.log;

  import Tone from 'tone';

  export default {
    data: function() {
      return {
        octave: '4',
        keys: [
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
        ],
        synth: {},
        noise: {}
      }
    },
    beforeMount: function(){
      this.synth = new Tone.Synth({
        oscillator: {
          type: "sawtooth",
          harmonicity: 0.5,
          modulationType: "sine"
        },
        envelope: {
          attackCurve: "exponential",
          attack: 0.05,
          decay: 0.8,
          sustain: 0.5,
          release: 2,
        },
        portamento: 0.2
      }).toMaster();
      // this.noise = new Tone.Noise("brown").toMaster().start(0).stop(3);
    },
    mounted: function() {

    },
    computed: {

    },
    methods: {
      octaveClass: function(n){
        return (this.octave == n) ? 'piano__octave-btn piano__octave-btn--active' : 'piano__octave-btn';
      },
      keyClass: function(clr){
        return (clr == 'black') ? 'piano__key piano__key--black' : 'piano__key';
      },
      changeOctive: function(o){
        this.octave = o;
      },
      playTone: function(note){
        this.synth.triggerAttackRelease(note, '8n');
      },
      playNoise: function(){
        // this.noise.volume.setValueAtTime(-20, 0)
      }
    }
  }

</script>
