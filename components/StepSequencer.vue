<template>
  <div>
    <p class="temphead">One Bar (16ths): </p>
    <div class="seq">
      <div v-for="k in 12" class="seq__keyrow">
        <node v-for="i in 16"
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
    <ul class="list list--inline list--left">
      <li class="list__item">
        <button @click="play()">
          {{ playing ? 'Pause' : 'Play' }}
        </button>
      </li>
      <li class="list__item">
        <button @click="clear()">
          Clear
        </button>
      </li>
      <li class="list__item">
        <button @click="reset()">
          Reset
        </button>
      </li>
      <li class="list__item">
        <button @click="logSynth()">
          Log Synth
        </button>
      </li>
    </ul>
    <div class="synth">
      <div v-if="synth" >
        <h2>Synth Properties:</h2>
        <ul>
          <li><b>Name: {{ synth }}</b></li>
          <li>
            Voices ({{ synth.voices.length }}):
            <ul>
              <li v-for="voice in synth.voices">
                {{ voice }} ({{ voice.oscillator.type }}):
                <label for="">Osc:</label>
                <select v-model="voice.oscillator.baseType">
                  <option value="sine">sine</option>
                  <option value="square">square</option>
                  <option value="sawtooth">sawtooth</option>
                  <option value="triangle">triangle</option>
                </select>
                <label for="">Partials:</label>
                <select v-model="voice.oscillator.partialCount">
                  <option value="0">0</option>
                  <option v-for="i in 8" :value="i">{{ i }}</option>
                </select>
                <ul>
                  <li>Envelope</li>
                  <li>Filter</li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </div>
      <div v-else>
        <i>No synth Loaded...</i>
      </div>
    </div>

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
        ri: 0, // render index (for clearing/re-setting)
        synth: false
      }
    },
    created: function(){
      var that = this;
      Tone.Transport.scheduleRepeat(function(){
        that.iteratePlay()
      }, "16n");
    },
    mounted: function(){
      this.createSynth(); // blank synth with default values
    },
    methods: {
      createSynth: function(){
        this.synth = new Tone.PolySynth(4, Tone.MonoSynth).toMaster();
        this.logSynth();
      },
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
      },
      logSynth: function(){
        console.log('=========');
        console.log(this.synth);
        console.log('=========');
      }
    }
  }
</script>
