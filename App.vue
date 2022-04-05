<template>
  <div v-if="this.ready">
    <div v-if="this.errorMessage" class="error" v-html="this.errorMessage.outerHTML"></div>
    <div v-else>
      <FirstScene v-if="this.active === this.scenesTypes.firstScene"/>
      <LinesScene v-if="this.active === this.scenesTypes.secondScene"/>
      <TextScene v-if="this.active === this.scenesTypes.thirdScene"/>
      <LoadModalScene v-if="this.active === this.scenesTypes.loadModelScene"/>
    </div>
  </div>

</template>

<script>
import FirstScene from './views/FirstScene.vue'
import {scenesTypes} from "./types/scenes.types";
import LinesScene from "./views/LinesScene";
import WebGL from "three/examples/jsm/capabilities/WebGL";
import TextScene from "./views/TextScene";
import LoadModalScene from "./views/LoadModalScene";

export default {
  ready: false,
  errorMessage: null,
  sceneTypes: scenesTypes,
  active: '',
  name: 'App',
  data() {
    return {
      name: '',
      errorMessage: null,
      scenesTypes: scenesTypes,
      active: '',
      ready: false,
    }
  },
  mounted() {
    if (!WebGL.isWebGLAvailable()) {
      this.errorMessage = WebGL.getWebGLErrorMessage();
    } else {
      this.active = scenesTypes.loadModelScene
    }
    this.ready = true;


  },
  components: {
    LoadModalScene,
    LinesScene,
    FirstScene,
    TextScene
  },
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0;
  margin: 0;
}
</style>
