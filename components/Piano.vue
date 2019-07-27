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
        :class="keyClass(key)"
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
    beforeMount: function(){
      this.synth = new Tone.Synth().toMaster();
      // Keyboards
      var that= this;
      document.addEventListener("keydown", function(event) {
        that.keys.forEach((key, index) => {
          if (key.code == event.which){
            that.keys[index].active = true;
            that.playTone(key.note + that.octave)
          }
        });
      })
      document.addEventListener("keyup", function(event) {
        that.keys.forEach((key, index) => {
          if (key.code == event.which){
            that.keys[index].active = false;
          }
        });
      })
    },
    mounted: function() {

    },
    computed: {

    },
    methods: {
      octaveClass: function(n){
        return (this.octave == n) ? 'piano__octave-btn piano__octave-btn--active' : 'piano__octave-btn';
      },
      keyClass: function(key){
        if (!key.active){
          return (key.color == 'black') ? 'piano__key piano__key--black' : 'piano__key';
        } else {
          return 'piano__key piano__key--blue'
        }
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
