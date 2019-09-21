<template>
  <div class="piano">

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
<<<<<<< HEAD
          { note: 'C', color: 'white', code: 65, active: false },
          { note: 'Db', color: 'black', code: 87, active: false },
          { note: 'D', color: 'white', code: 83, active: false },
          { note: 'Eb',color: 'black', code: 69, active: false },
          { note: 'E', color: 'white', code: 68, active: false },
          { note: 'F', color: 'white', code: 70, active: false },
          { note: 'Gb', color: 'black', code: 84, active: false },
          { note: 'G', color: 'white', code: 71, active: false },
          { note: 'Ab', color: 'black', code: 89, active: false },
          { note: 'A', color: 'white', code: 72, active: false },
          { note: 'Bb', color: 'black', code: 85, active: false },
          { note: 'B', color: 'white', code: 74, active: false }
=======
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
>>>>>>> origin/step-sequencer
        ],
        synth: {},
        noise: {}
      }
    },
<<<<<<< HEAD
    created: function(){
      this.synth = new Tone.PolySynth(4, Tone.MonoSynth, {
            "oscillator" : {
                "type" : "square8"
            },
            "envelope" : {
                "attack" : 0.05,
                "decay" : 0.3,
                "sustain" : 0.4,
                "release" : 0.8,
            },
            "filterEnvelope" : {
                "attack" : 0.001,
                "decay" : 0.7,
                "sustain" : 0.1,
                "release" : 1.8,
                "baseFrequency" : 300,
                "octaves" : 4
            }
        }).toMaster();
=======
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
>>>>>>> origin/step-sequencer
    },
    mounted: function() {
      var that = this;
      Tone.Transport.scheduleRepeat(function(time){
	       that.synth.triggerAttackRelease('C4', '8n');
      }, "2n");
      Tone.Transport.start()
    },
    computed: {

    },
    methods: {
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
