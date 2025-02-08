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
    { id: 1, src: new URL('src/assets/2cw_0029_Cassa1.png', import.meta.url).href },
    { id: 2, src: new URL('../assets/2cw_0028_Cassa2.png', import.meta.url).href }
  ],
  ring: [
    { id: 1, src: new URL('@/assets/2cw_0027_Ghiera1.png', import.meta.url).href },
    { id: 2, src: new URL('@/assets/2cw_0026_Ghiera2.png', import.meta.url).href },
    { id: 3, src: new URL('@/assets/2cw_0025_Ghiera3.png', import.meta.url).href },
    { id: 4, src: new URL('@/assets/2cw_0024_Ghiera4.png', import.meta.url).href },
    { id: 5, src: new URL('@/assets/2cw_0023_Ghiera5.png', import.meta.url).href },
    { id: 6, src: new URL('@/assets/2cw_0022_Ghiera6.png', import.meta.url).href },
    { id: 7, src: new URL('@/assets/2cw_0021_Ghiera7.png', import.meta.url).href },
    { id: 8, src: new URL('@/assets/2cw_0020_Ghiera8.png', import.meta.url).href },
    { id: 9, src: new URL('@/assets/2cw_0019_Ghiera9.png', import.meta.url).href },
    { id: 10, src: new URL('@/assets/2cw_0018_Ghiera10.png', import.meta.url).href },
    { id: 11, src: new URL('@/assets/2cw_0017_Ghiera11.png', import.meta.url).href },
    { id: 12, src: new URL('@/assets/2cw_0016_Ghiera12.png', import.meta.url).href },
    { id: 13, src: new URL('@/assets/2cw_0015_Ghiera13.png', import.meta.url).href },
    { id: 14, src: new URL('@/assets/2cw_0014_Ghiera14.png', import.meta.url).href },
    { id: 15, src: new URL('@/assets/2cw_0013_Ghiera15.png', import.meta.url).href }
  ],
  bezel: [
    { id: 1, src: new URL('@/assets/2cw_0012_Quadrante1.png', import.meta.url).href },
    { id: 2, src: new URL('@/assets/2cw_0011_Quadrante2.png', import.meta.url).href },
    { id: 3, src: new URL('@/assets/2cw_0010_Quadrante3.png', import.meta.url).href }
  ],
  dial: [
    { id: 1, src: new URL('@/assets/2cw_0009_Lancette1.png', import.meta.url).href },
    { id: 2, src: new URL('@/assets/2cw_0008_Lancette2.png', import.meta.url).href },
    { id: 3, src: new URL('@/assets/2cw_0007_Lancette3.png', import.meta.url).href },
    { id: 4, src: new URL('@/assets/2cw_0006_Lancette4.png', import.meta.url).href },
    { id: 5, src: new URL('@/assets/2cw_0005_Lancette5.png', import.meta.url).href },
    { id: 6, src: new URL('@/assets/2cw_0004_Lancette6.png', import.meta.url).href },
    { id: 7, src: new URL('@/assets/2cw_0003_Lancette7.png', import.meta.url).href },
    { id: 8, src: new URL('@/assets/2cw_0002_Lancette8.png', import.meta.url).href },
    { id: 9, src: new URL('@/assets/2cw_0001_Lancette9.png', import.meta.url).href },
    { id: 10, src: new URL('@/assets/2cw_0000_Lancette10.png', import.meta.url).href }
  ]
});

const configuration = ref({
  case: configurations.value.case.length > 0 ? configurations.value.case[0].id : null,
  ring: configurations.value.ring.length > 0 ? configurations.value.ring[0].id : null,
  bezel: configurations.value.bezel.length > 0 ? configurations.value.bezel[0].id : null,
  dial: configurations.value.dial.length > 0 ? configurations.value.dial[0].id : null
});

const setLayer = (layer, direction) => {
  const items = configurations.value[layer];
  if (!items || items.length === 0) return;
  const currentIndex = items.findIndex(item => item.id === configuration.value[layer]);
  let newIndex = currentIndex + direction;
  if (newIndex >= items.length) newIndex = 0;
  if (newIndex < 0) newIndex = items.length - 1;
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
  <div class="container configurator d-flex flex-column align-items-center justify-content-center" :class="{ 'debug': settings.debug }">
    <pre v-if="settings.debug">{{ configuration }}</pre>
    <h1>Configurator</h1>
    <div class="layers" :style="{ width: settings.layerWidth + 'px', height: settings.layerHeight + 'px' }">
      <ConfiguratorLayer name="ring" />  
      <ConfiguratorLayer name="case" />    
      <ConfiguratorLayer name="bezel" />
      <ConfiguratorLayer name="dial" />
    </div>
    <div class="controls">
      <div class="control case">
        <button @click="setLayer('case', -1)">Prev</button>
        <button @click="setLayer('case', 1)">Next</button>
      </div>
      <div class="control ring">
        <button @click="setLayer('ring', -1)">Prev</button>
        <button @click="setLayer('ring', 1)">Next</button>
      </div>
      <div class="control bezel">
        <button @click="setLayer('bezel', -1)">Prev</button>
        <button @click="setLayer('bezel', 1)">Next</button>
      </div>
      <div class="control dial">
        <button @click="setLayer('dial', -1)">Prev</button>
        <button @click="setLayer('dial', 1)">Next</button>
      </div>
    </div>
  </div>
</template>

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
      .controls {
        position: absolute;
        bottom: -50px;
        width: 100%;
        text-align: center;
      }
      &.ring {
        z-index: 3;
      }
      &.case {
        z-index: 2;
      }
      &.bezel {
        z-index: 1;
      }
      &.dial {
        z-index: 0;
      }
    }
  }

  &.debug {
    border: 1px solid blue;
    .layers {
      overflow: visible;
      .layer {
        border: 1px solid red;
        &.ring img, &.bezel img, &.dial img {
          opacity: 0.5;
        }
      }
    }
    .controls {
      border: 1px solid green;
    }
  }
}
</style>
