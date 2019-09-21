<template>
  <div class="seq">
    <div v-for="k in 12" class="seq__keyrow">
      <node v-for="i in 8" />
    </div>
  </div>
</template>

<script>
  import Node from '~/components/StepSequencer/Node.vue'
  export default {
    components: {
      Node
    },
    data: function(){
      return {}
    }
  }
</script>
