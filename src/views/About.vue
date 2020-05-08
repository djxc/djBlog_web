<template>
  <div class="about">
    <editor></editor>
  </div>
</template>
<script lang="ts">
import Vue from 'vue'
import editor from '@/components/editor.vue'
export default Vue.extend({
  name:"about",
  components: {
    editor
  }
})
</script>
