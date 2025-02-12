<script setup>
import { ref, onMounted, provide } from 'vue';
import ConfiguratorLayer from './configurator-layer.vue';

const settings = ref({
  layerWidth: 500,
  layerHeight: 600,
  debug: true,
});

const configurations = ref({
  case: [
    { id: 1, src: '/assets/2cw_0029_Cassa1.png' },
    { id: 2, src: '/assets/2cw_0028_Cassa2.png' }
  ],
  ring: [
    { id: 1, src: '/assets/2cw_0027_Ghiera1.png' },
    { id: 2, src: '/assets/2cw_0026_Ghiera2.png' },
    { id: 3, src: '/assets/2cw_0025_Ghiera3.png' },
    { id: 4, src: '/assets/2cw_0024_Ghiera4.png' },
    { id: 5, src: '/assets/2cw_0023_Ghiera5.png' },
    { id: 6, src: '/assets/2cw_0022_Ghiera6.png' },
    { id: 7, src: '/assets/2cw_0021_Ghiera7.png' },
    { id: 8, src: '/assets/2cw_0020_Ghiera8.png' },
    { id: 9, src: '/assets/2cw_0019_Ghiera9.png' },
    { id: 10, src: '/assets/2cw_0018_Ghiera10.png' },
    { id: 11, src: '/assets/2cw_0017_Ghiera11.png' },
    { id: 12, src: '/assets/2cw_0016_Ghiera12.png' },
    { id: 13, src: '/assets/2cw_0015_Ghiera13.png' },
    { id: 14, src: '/assets/2cw_0014_Ghiera14.png' },
    { id: 15, src: '/assets/2cw_0013_Ghiera15.png' }
  ],
  bezel: [
    { id: 1, src: '/assets/2cw_0012_Quadrante1.png' },
    { id: 2, src: '/assets/2cw_0011_Quadrante2.png' },
    { id: 3, src: '/assets/2cw_0010_Quadrante3.png' }
  ],
  dial: [
    { id: 1, src: '/assets/2cw_0009_Lancette1.png' },
    { id: 2, src: '/assets/2cw_0008_Lancette2.png' },
    { id: 3, src: '/assets/2cw_0007_Lancette3.png' },
    { id: 4, src: '/assets/2cw_0006_Lancette4.png' },
    { id: 5, src: '/assets/2cw_0005_Lancette5.png' },
    { id: 6, src: '/assets/2cw_0004_Lancette6.png' },
    { id: 7, src: '/assets/2cw_0003_Lancette7.png' },
    { id: 8, src: '/assets/2cw_0002_Lancette8.png' },
    { id: 9, src: '/assets/2cw_0001_Lancette9.png' },
    { id: 10, src: '/assets/2cw_0000_Lancette10.png' }
  ]
});

const configuration = ref({
  case: configurations.value.case[0]?.id || null,
  ring: configurations.value.ring[0]?.id || null,
  bezel: configurations.value.bezel[0]?.id || null,
  dial: configurations.value.dial[0]?.id || null
});

const setLayer = (layer, direction) => {
  const items = configurations.value[layer];
  if (!items || items.length === 0) return;
  const currentIndex = items.findIndex(item => item.id === configuration.value[layer]);
  let newIndex = (currentIndex + direction + items.length) % items.length;
  configuration.value[layer] = items[newIndex].id;
};

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search);
  if (urlParams.has('debug')) {
    settings.value.debug = true;
  }
});



provide('settings', settings);
provide('configurations', configurations);
provide('configuration', configuration);
</script>

<template>
  <div class="container configurator d-flex flex-column align-items-center justify-content-center" 
     :style="{ backgroundColor: backgroundColor }"
     :class="{ 'debug': settings.debug }">
    <pre v-if="settings.debug">{{ configuration }}</pre>
    <h1>Configurator</h1>
    <div class="layers" :style="{ width: settings.layerWidth + 'px', height: settings.layerHeight + 'px' }">
      <ConfiguratorLayer name="case" />    
      <ConfiguratorLayer name="bezel" />
      <ConfiguratorLayer name="ring" />  
      <ConfiguratorLayer name="dial" />
    </div>
    <nav class="navbar">
      <button v-for="(level, index) in levels" :key="index" @click="selectedLevel = level"
        :class="{ active: selectedLevel === level }">
        {{ level }}
      </button>
    </nav>
    <div class="controls">
      <button @click="setLayer(selectedLevel, -1)">Prev</button>
      <button @click="setLayer(selectedLevel, 1)">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      levels: ["case", "bezel", "ring", "dial"],
      selectedLevel: "case"
    };
  }
};
</script>

<style lang="scss" scoped>
.configurator {
  padding: 0;
  margin: 0;
  .layers {
    position: relative;
    overflow: hidden;
    .layer {
      position: absolute;
      width: 100%;
      height: 100%;
      display: flex;
      transition: transform 0.5s ease-in-out;
      &.case { z-index: 0; }
      &.bezel { z-index: 1; }
      &.ring { z-index: 2; }
      &.dial { z-index: 3; }
    }
  }

  .navbar {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-bottom: 20px;
  }
  .navbar button {
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    background: #ddd;
    font-size: 16px;
  }
  .navbar button.active {
    background: #333;
    color: white;
  }
  .controls {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 20px;
  }
  .controls button {
    padding: 10px;
    background: #333;
    color: white;
    border: none;
    cursor: pointer;
  }
}
</style>
