<template>
  <div>
    <div class="seq">
      <div v-for="k in 12" class="seq__keyrow">
        <node v-for="i in 8" v-bind:row="i" v-bind:step="step" />
      </div>
    </div>
    <button class="play" @click="play">
      Play
    </button>
  </div>
</template>

<script>
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
