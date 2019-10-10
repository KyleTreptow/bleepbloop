<template>
  <div class="synth">
    <div v-if="synth">
      <p class="synth__title">
        <b>Name:</b> {{ name }} - {{ synth }}
      </p>
      <div class="#">
        <select v-model="note.value">
          <option v-for="t in tones" :value="t">{{ t }}</option>
        </select>
        <select v-model="note.octave">
          <option v-for="i in 8" :value="i - 4">{{ i - 4 }}</option>
        </select>
        <select v-model="note.duration">
          <option v-for="d in durations" :value="d">{{ d }}</option>
        </select>
        <button @click="playNote(note.value, note.octave, note.duration)">
          Play: {{ note.value + note.octave + ' for '+note.duration }}
        </button>
      </div>
      <div class="synth__details">
        <div class="synth__module">
          <h4>Oscillator:</h4>
          <div class="synth__panel">
            <label for="">Type:</label> &nbsp;
            <select v-model="synth.oscillator.baseType">
              <option value="sine">sine</option>
              <option value="square">square</option>
              <option value="sawtooth">sawtooth</option>
              <option value="triangle">triangle</option>
            </select>
            &nbsp;
            <label for="">Partials:</label> &nbsp;
            <select v-model="synth.oscillator.partialCount">
              <option value=""></option>
              <!-- <option value="0">0</option> -->
              <option v-for="i in 32" :value="i">{{ i }}</option>
            </select>
            &nbsp;
            <label for="">Detune:</label> &nbsp;
            <input type="number" v-model="synth.oscillator.detune.value"
            min="-20" max="20" />
          </div>
          <h4>Amp Env (A, D, S, R):</h4>
          <div class="synth__panel">
            A: &nbsp; <input v-model="synth.envelope.attack"
              type="range" min="0.005" max="2.0" step="0.005" />
            &nbsp; <label for="">{{ synth.envelope.attack }}</label> <br>
            D: &nbsp; <input v-model="synth.envelope.decay"
              type="range" min="0.2" max="1.0" step="0.1" />
            &nbsp; <label for="">{{ synth.envelope.decay }}</label> <br>
            S: &nbsp; <input v-model="synth.envelope.sustain"
              type="range" min="0.5" max="5.0" step="0.5" />
            &nbsp; <label for="">{{ synth.envelope.sustain }}</label> <br>
            R: &nbsp; <input v-model="synth.envelope.release"
              type="range" min="0.1" max="5.0" step="0.1" />
            &nbsp; <label for="">{{ synth.envelope.release }}</label>
          </div>
        </div>
        <div class="synth__module">
          <h4>Filter:</h4>
          <div class="synth__panel">
            Type: &nbsp;
            <select v-model="synth.filter.type">
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
            <select v-model="synth.filter.rolloff">
              <option value="-12">-12</option>
              <option value="-24">-24</option>
              <option value="-48">-48</option>
              <option value="-96">-96</option>
            </select>
            &nbsp;
            Q: &nbsp;
            <select v-model="synth.filter.Q.value">
              <option v-for="i in 6" :value="i">{{ i }}</option>
            </select>
          </div>
          <div class="synth__panel">
            Freq: &nbsp;
            <input v-model="synth.filter.frequency.value" type="range"
            min="0" max="40000" step="100" />
            &nbsp;
            {{ formatNumCommas(synth.filter.frequency.value) }} hz
          </div>
          <h4>Filter Env (A, D, S, R):</h4>
          <div class="synth__panel">
            A: &nbsp; <input v-model="synth.filterEnvelope.attack"
              type="range" min="0.005" max="1.0" step="0.005" />
            &nbsp; <label for="">{{ synth.filterEnvelope.attack }}</label> <br>
            D: &nbsp; <input v-model="synth.filterEnvelope.decay"
              type="range" min="0.2" max="1.0" step="0.1" />
            &nbsp; <label for="">{{ synth.filterEnvelope.decay }}</label> <br>
            S: &nbsp; <input v-model="synth.filterEnvelope.sustain"
              type="range" min="0.5" max="5.0" step="0.5" />
            &nbsp; <label for="">{{ synth.filterEnvelope.sustain }}</label> <br>
            R: &nbsp; <input v-model="synth.filterEnvelope.release"
              type="range" min="0.1" max="5.0" step="0.1" />
            &nbsp; <label for="">{{ synth.filterEnvelope.release }}</label>
          </div>
        </div>
        <div class="synth__module">
          Module 3
        </div>
      </div>
      <div class="#">
        <button @click="log(synth)">Log Synth to Console...</button>
        <button @click="killSynth()">Kill Synth</button>
      </div>
    </div>
    <div v-else>
      <p class="synth__title">
        <b>No Synth Loaded</b> <br>
        <i>Create a synth...</i>
      </p>
      <div class="#">
        <button @click="createSynth()">Create Synth</button>
      </div>
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
      tones: ['C', 'Db', 'D', 'Eb', 'E', 'F', 'Gb', 'G', 'Ab', 'A', 'Bb', 'B'],
      durations: ['1n', '2n', '4n', '8n', '16n'],
      synth: false,
      config: {},
      voices: 1,
      note: {
        value: 'C',
        octave: '4',
        duration: '16n'
      }
    }
  },
  created: function(){
    this.createSynth();
  },
  mounted: function(){
    // on mounted
  },
  computed: {
    // computed values here
  },
  methods: {
    playNote: function(v, o, d){
      this.synth.triggerAttackRelease(String(v+o), d);
    },
    log: function(data){
      console.log(data);
    },
    createSynth: function(){
      this.synth = new Tone.MonoSynth().toMaster();
    },
    killSynth: function(){
      this.synth = false;
    },
    formatNumCommas: function(num){
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  }
}
</script>

<style lang="sass">

</style>
