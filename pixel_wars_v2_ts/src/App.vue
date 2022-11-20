<template> 
  <div id="root">
    <div class="main-card">
      <div class="header">
        <h1> Pixel warS </h1>
      </div>
      <Field
        v-model:pixelSize = "processData.pixelSize"
        @updatePixelGrid="processData.gridCoordColors"
      />
    </div>
  </div>
</template>

<script lang="ts">
  import Field from './components/Field.vue';
  export default {
    components:  { Field },

    data() {
      return {
        screenHeight: screen.availHeight,
        processData: {
          pixelSize: 80,
          gridCoordColors: [],
        }
      };
    },
  }
</script>

<style>

  #root {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  .header {
    height: 5%;
    width: auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .header h1 {
    font-size: 35px;
    line-height: 30px;
    letter-spacing: 8px;
    font-family: monospace;
  }
</style>
