<template>
  <div>
    <div class="seq">
      <h1 class="seq__title">One Bar (16ths): </h1>
      <div class="seq__body">
        <div v-for="k in 12" class="seq__keyrow">
          <node v-for="i in 16"
            :data-key="k+'-'+i+'-'+ri"
            :data-step="step"
            :key="k+'-'+i+'-'+ri"
            :col="k"
            :row="i"
            :step="step"
            :synth="synth"
            :random="(random[k -1][i -1]) ? random[k -1][i -1] : false"
          />
        </div>
      </div>
      <ul class="list list--inline list--left" v-if="synth">
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
          <button @click="generateRandom(true)">
            Random Notes
          </button>
        </li>
      </ul>
    </div>

    <!-- Start Synth -->
    <div class="synth">
      <div v-if="synth" >
        <p class="synth__title">
          <b>{{ synth }}</b>
          ({{ synth.voices.length + (synth.voices.length == 1 ? ' voice' : ' voices') }}):
        </p>
        <ul class="list list--inline list--left">
          <li class="list__item">
            <button @click="createSynth(synthVoices)">
              {{ synth ? 'Reset' : 'Create'}} Synth
            </button>
            <label class="control__label" for="#">Voices:</label>
            <input type="number" v-model="synthVoices"
            min="0" max="6" step="1" />
          </li>
          <li class="list__item">
            <button @click="log(synth, 'PolySynth Log: ')">
              Log Synth to Console
            </button>
          </li>
        </ul>
        <ul>
          <!-- Start Voice -->
          <li v-for="(voice, index) in synth.voices" class="synth__voice">
            <ul class="synth__details">
              <li class="synth__module">
                <h4>{{ '#'+(index + 1)+'. ' }} {{ voice }} ({{ voice.oscillator.type }}):</h4>
                <div class="synth__panel">
                  <label for="">Osc:</label> &nbsp;
                  <select v-model="voice.oscillator.baseType">
                    <option value="sine">sine</option>
                    <option value="square">square</option>
                    <option value="sawtooth">sawtooth</option>
                    <option value="triangle">triangle</option>
                  </select>
                  &nbsp;
                  <label for="">Partials:</label> &nbsp;
                  <select v-model="voice.oscillator.partialCount">
                    <option value=""></option>
                    <!-- <option value="0">0</option> -->
                    <option v-for="i in 32" :value="i">{{ i }}</option>
                  </select>
                  &nbsp;
                  <label for="">Detune:</label> &nbsp;
                  <input type="number" v-model="voice.oscillator.detune.value"
                  min="-20" max="20" />
                </div>
                <h4>Amp Env (A, D, S, R):</h4>
                <div class="synth__panel">
                  A: &nbsp; <input v-model="voice.envelope.attack"
                    type="range" min="0.005" max="2.0" step="0.005" />
                  &nbsp; <label for="">{{ voice.envelope.attack }}</label> <br>
                  D: &nbsp; <input v-model="voice.envelope.decay"
                    type="range" min="0.2" max="1.0" step="0.1" />
                  &nbsp; <label for="">{{ voice.envelope.decay }}</label> <br>
                  S: &nbsp; <input v-model="voice.envelope.sustain"
                    type="range" min="0.5" max="5.0" step="0.5" />
                  &nbsp; <label for="">{{ voice.envelope.sustain }}</label> <br>
                  R: &nbsp; <input v-model="voice.envelope.release"
                    type="range" min="0.1" max="5.0" step="0.1" />
                  &nbsp; <label for="">{{ voice.envelope.release }}</label>
                </div>
              </li>
              <li class="synth__module">
                <h4>Filter:</h4>
                <div class="synth__panel">
                  Type: &nbsp;
                  <select v-model="voice.filter.type">
                    <option value="lowpass">lowpass</option>
                    <option value="highpass">highpass</option>
                    <option value="bandpass">bandpass</option>
                    <option value="lowshelf">lowshelf</option>
                    <option value="highshelf">highshelf</option>
                    <option value="notch">notch</option>
                    <option value="allpass">allpass</option>
                    <option value="peaking">peaking</option>
                  </select>
                  &nbsp;
                  Rolloff: &nbsp;
                  <select v-model="voice.filter.rolloff">
                    <option value="-12">-12</option>
                    <option value="-24">-24</option>
                    <option value="-48">-48</option>
                    <option value="-96">-96</option>
                  </select>
                  &nbsp;
                  Q: &nbsp;
                  <select v-model="voice.filter.Q.value">
                    <option v-for="i in 6" :value="i">{{ i }}</option>
                  </select>
                </div>
                <div class="synth__panel">
                  Freq: &nbsp;
                  <input v-model="voice.filter.frequency.value" type="range"
                  min="0" max="40000" step="100" />
                  &nbsp;
                  {{ formatNumCommas(voice.filter.frequency.value) }} hz
                </div>
                <h4>Filter Env (A, D, S, R):</h4>
                <div class="synth__panel">
                  A: &nbsp; <input v-model="voice.filterEnvelope.attack"
                    type="range" min="0.005" max="1.0" step="0.005" />
                  &nbsp; <label for="">{{ voice.filterEnvelope.attack }}</label> <br>
                  D: &nbsp; <input v-model="voice.filterEnvelope.decay"
                    type="range" min="0.2" max="1.0" step="0.1" />
                  &nbsp; <label for="">{{ voice.filterEnvelope.decay }}</label> <br>
                  S: &nbsp; <input v-model="voice.filterEnvelope.sustain"
                    type="range" min="0.5" max="5.0" step="0.5" />
                  &nbsp; <label for="">{{ voice.filterEnvelope.sustain }}</label> <br>
                  R: &nbsp; <input v-model="voice.filterEnvelope.release"
                    type="range" min="0.1" max="5.0" step="0.1" />
                  &nbsp; <label for="">{{ voice.filterEnvelope.release }}</label>
                </div>
              </li>
              <li class="synth__module">
                <h4>Master Volume:</h4>
                <div class="synth__panel">
                  <input v-model="voice.volume.value" type="range"
                  min="-10.0" max="10.0" step="0.5" />
                  &nbsp;
                  <label for="">
                    {{ (Math.round(voice.volume.value * 100) / 100) + ' ' + voice.volume.units }}
                  </label>
                </div>
                <h4>Other Options:</h4>
                <div class="synth__panel">
                  <button @click="log(voice, 'Mono Voice Log: ')">Log Voice to Console</button>
                </div>
              </li>
            </ul>
          </li>
          <!-- End Voice -->
        </ul>
      </div>
      <div v-else>
        <p class="synth__title">
          <b>No Synth Loaded</b> <br>
          <i>Create a synth with at least one voice.</i>
        </p>
        <ul class="list list--inline list--left">
          <li class="list__item">
            <button @click="createSynth(synthVoices)">
              {{ synth ? 'Reset' : 'Create'}} Synth
            </button>
            <label class="control__label" for="#">Voices:</label>
            <input type="number" v-model="synthVoices"
            min="0" max="6" step="1" />
          </li>
        </ul>
      </div>
    </div>
    <!-- End Synth -->

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
        synth: false,
        synthVoices: 1,
        random: false
      }
    },
    created: function(){
      var that = this;
      // create array (false to set all cells as false)
      this.generateRandom(false);
      // Tone
      Tone.Transport.scheduleRepeat(function(){
        that.iteratePlay()
      }, "16n");
    },
    mounted: function(){
      this.createSynth(this.synthVoices); // blank synth with default values
    },
    computed: {
      // none...
    },
    methods: {
      createSynth: function(v){
        if(v == 0){
          this.synth = false;
        } else {
          this.synth = new Tone.PolySynth(v, Tone.MonoSynth).toMaster();
          this.log(this.synth, 'Init Synth Log: ');
        }
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
        this.ri++;
        this.generateRandom(false);
      },
      reset: function(){
        Tone.Transport.stop();
        this.playing = false;
        this.step = 0;
        this.clear();
      },
      generateRandom: function(active){
        // if active is set to false, it clears out the random notes...
        var that = this;
        // create array
        var randArray = new Array(12);
        for (var k = 0; k < randArray.length; k++) {
          randArray[k] = new Array(16);
          for (var i = 0; i < randArray[k].length; i++) {
            var num = Math.floor(Math.random() * Math.floor(18));
            if(num === 1 && active){
              randArray[k][i] = true;
            } else {
              randArray[k][i] = false;
            }
          }
        }
        this.ri++; // clear...
        this.random = randArray;
      },
      iteratePlay: function(){
        if (this.step < 16){ this.step = this.step + 1 }
        else { this.step = 1 }
      },
      log: function(data, msg){
        if(msg){
          console.log(msg);
        }
        console.log(data);
        console.log('=========');
      },
      formatNumCommas: function(num){
        return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
    }
  }
</script>
