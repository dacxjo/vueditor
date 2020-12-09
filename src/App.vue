<template>
  <main class="w-full h-screen flex">
      <toolbar class="w-16"></toolbar>
      <canvas-field class="w-full"></canvas-field>
  </main>
</template>

<script>

import Toolbar from './components/Toolbar.vue'
import CanvasField from './components/CanvasField.vue'

export default {
  name: 'VueDitor',
  components: {
    Toolbar,
    CanvasField
  }
}
</script>
