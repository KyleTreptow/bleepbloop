<template>
  <div>
    <div class="seq">
      <div v-for="k in 12" class="seq__keyrow">
        <node
          v-for="i in 8"
          v-bind:col="k"
          v-bind:row="i"
          v-bind:step="step"
          v-bind:synth="synth"
        />
      </div>
    </div>
    <button class="play" @click="play">
      Play
    </button>
  </div>
</template>

<script>
  import Tone from 'tone';
  import Node from '~/components/StepSequencer/Node.vue'
  export default {
    components: {
      Node
    },
    data: function(){
      return {
        step: 0
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
    methods: {
      play: function(){
        this.iteratePlay()
      },
      iteratePlay: function(){
        if (this.step < 8){ this.step = this.step + 1 }
        else { this.step = 1 }
        console.log(this.step)
      }
    }
  }
</script>
