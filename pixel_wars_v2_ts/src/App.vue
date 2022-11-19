<template> 
  <div id="root">
    <div class="main-card">
      <div class="header">
        <h1> Pixel warS </h1>
      </div>
      <Field
        :pixelSize = "processData.pixelSize"
        v-model:setPixelSizeField="processData.pixelSize"
      />
      <div class="settings">
        <my-form
          v-model:setPixelSizeForm="processData.pixelSize"
          :formID="'change-pixel-size-form'"
        />
      </div>
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
          pixelSize: 6,
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
  .settings {
    display: flex;
    justify-content: end;
  }
</style>
