<template>
  <div>
    <p class="temphead">One Bar (16ths): </p>
    <div class="seq">
      <div v-for="k in 12" class="seq__keyrow">
        <node
          v-for="i in 16"
          :data-key="k+'-'+i+'-'+ri"
          :data-step="step"
          :key="k+'-'+i+'-'+ri"
          :col="k"
          :row="i"
          :step="step"
          :synth="synth"
        />
      </div>
    </div>
    <button @click="play()">
      {{ playing ? 'Pause' : 'Play' }}
    </button>
    <button @click="clear()">
      Clear
    </button>
    <button @click="reset()">
      Reset
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
        step: 0,
        playing: false,
        ri: 0 // render index
      }
    },
    created: function(){
      var that = this
      Tone.Transport.scheduleRepeat(function(){
         that.iteratePlay()
      }, "16n");
      this.synth = new Tone.PolySynth(6, Tone.MonoSynth, {
            "oscillator" : {
                "type" : "square4"
            },
            "envelope" : {
                "attack" : 0.5,
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
        if (!this.playing){
          Tone.Transport.start()
          this.playing = true
        } else {
          Tone.Transport.stop()
          this.playing = false
        }
      },
      clear: function(){
        this.ri++
      },
      reset: function(){
        Tone.Transport.stop()
        this.playing = false
        this.step = 0
        this.clear()
      },
      iteratePlay: function(){
        if (this.step < 16){ this.step = this.step + 1 }
        else { this.step = 1 }
        // console.log(this.step)
      }
    }
  }
</script>
