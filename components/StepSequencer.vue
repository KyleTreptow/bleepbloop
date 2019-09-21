<template>
  <div class="seq">
    <div v-for="k in 12" class="seq__keyrow">
      <span v-for="i in 8" class="seq__bar">
        Bar
      </span>
    </div>
  </div>
</template>

<script>
  export default {
    data: function(){
      return {}
    }
  }
</script>
