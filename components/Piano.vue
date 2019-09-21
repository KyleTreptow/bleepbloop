<template>
  <div class="piano">

  </div>
</template>

<script>

  import Tone from 'tone';

  export default {
    data: function() {
      return {
        octave: '4',
        keys: [
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
        ],
        synth: {},
        noise: {}
      }
    },
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
