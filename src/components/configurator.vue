<script setup>
import { ref, onMounted, provide, computed, watch } from 'vue';
import ConfiguratorLayer from './configurator-layer.vue';

const backgroundColor = ref('#0A001D');

onMounted(() => {
  document.body.style.backgroundColor = backgroundColor.value;

  const modelConfig = configurations.value[selectedModel.value];
  const initial = {};
  for (const key in modelConfig) {
    initial[key] = modelConfig[key][0]?.id || null;
  }
  configuration.value = initial;

  document.title = `2CW Configurator - ${selectedModel.value.toUpperCase()}`;

  const urlParams = new URLSearchParams(window.location.search);
  if (urlParams.has('debug')) {
    settings.value.debug = true;
  }
});

const settings = ref({
  layerWidth: 375,
  layerHeight: 450,
  debug: false,
});

const configurations = ref({
  seasub: {
    case: [
      { id: 1, src: '/assets/2cw_0034_Cassa1.png' },
      { id: 2, src: '/assets/2cw_0033_Cassa2.png' },
      { id: 3, src: '/assets/2cw_0032_Cassa3.png' },
      { id: 4, src: '/assets/2cw_0031_Cassa4.png' }
    ],
    ring: [
      { id: 1, src: '/assets/2cw_0016_Ghiera1.png' },
      { id: 2, src: '/assets/2cw_0017_Ghiera2.png' },
      { id: 3, src: '/assets/2cw_0018_Ghiera3.png' },
      { id: 4, src: '/assets/2cw_0019_Ghiera4.png' },
      { id: 5, src: '/assets/2cw_0020_Ghiera5.png' },
      { id: 6, src: '/assets/2cw_0021_Ghiera6.png' },
      { id: 7, src: '/assets/2cw_0022_Ghiera7.png' },
      { id: 8, src: '/assets/2cw_0023_Ghiera8.png' },
      { id: 9, src: '/assets/2cw_0024_Ghiera9.png' },
      { id: 10, src: '/assets/2cw_0025_Ghiera10.png' },
      { id: 11, src: '/assets/2cw_0026_Ghiera11.png' },
      { id: 12, src: '/assets/2cw_0027_Ghiera12.png' },
      { id: 13, src: '/assets/2cw_0028_Ghiera13.png' },
      { id: 14, src: '/assets/2cw_0029_Ghiera14.png' },
      { id: 15, src: '/assets/2cw_0030_Ghiera15.png' }
    ],
    bezel: [
      { id: 1, src: '/assets/2cw_0015_Quadrante3.png' },
      { id: 2, src: '/assets/2cw_0014_Quadrante2.png' },
      { id: 3, src: '/assets/2cw_0013_Quadrante1.png' },
    ],
    dial: [
      { id: 1, src: '/assets/2cw_0009_Lancette1.png' },
      { id: 2, src: '/assets/2cw_0008_Lancette9.png' },
      { id: 3, src: '/assets/2cw_0007_Lancette8.png' },
      { id: 4, src: '/assets/2cw_0006_Lancette7.png' },
      { id: 5, src: '/assets/2cw_0005_Lancette6.png' },
      { id: 6, src: '/assets/2cw_0004_Lancette5.png' },
      { id: 7, src: '/assets/2cw_0003_Lancette4.png' },
      { id: 8, src: '/assets/2cw_0002_Lancette3.png' },
      { id: 9, src: '/assets/2cw_0001_Lancette10.png' },
      { id: 10, src: '/assets/2cw_0010_Lancette11.png' },
      { id: 11, src: '/assets/2cw_0011_Lancette12.png' },
      { id: 12, src: '/assets/2cw_0012_Lancette2.png' }
    ],
    strap: [
      { id: 1, src: '/assets/2cw_0054_Cinturino1.png' },
      { id: 2, src: '/assets/2cw_0055_Cinturino2.png' },
      { id: 3, src: '/assets/2cw_0048_Cinturino3.png' },
      { id: 4, src: '/assets/2cw_0050_Cinturino4.png' },
      { id: 5, src: '/assets/2cw_0044_Cinturino5.png' },
      { id: 6, src: '/assets/2cw_0052_Cinturino6.png' },
      { id: 7, src: '/assets/2cw_0046_Cinturino7.png' },
      { id: 8, src: '/assets/2cw_0051_Cinturino8.png' },
      { id: 9, src: '/assets/2cw_0043_Cinturino9.png' },
      { id: 10, src: '/assets/2cw_0053_Cinturino10.png' },
      { id: 11, src: '/assets/2cw_0045_Cinturino11.png' },
      { id: 12, src: '/assets/2cw_0049_Cinturino12.png' },
      { id: 13, src: '/assets/2cw_0047_Cinturino13.png' },
      { id: 14, src: '/assets/2cw_0041_Cinturino14.png' },
      { id: 15, src: '/assets/2cw_0035_Cinturino15.png' },
      { id: 16, src: '/assets/2cw_0036_Cinturino16.png' },
      { id: 17, src: '/assets/2cw_0042_Cinturino17.png' },
      { id: 18, src: '/assets/2cw_0037_Cinturino18.png' },
      { id: 19, src: '/assets/2cw_0038_Cinturino19.png' }
    ]
  },
  jetlag: {
    case: [
      { id: 1, src: '/assets/2cw_0034_Cassa1.png' },
      { id: 2, src: '/assets/2cw_0033_Cassa2.png' },
      { id: 3, src: '/assets/2cw_0032_Cassa3.png' },
      { id: 4, src: '/assets/2cw_0031_Cassa4.png' }
    ],
    ring: [
      { id: 1, src: '/assets/2cw_0017_GhieraGMT1.png' },
      { id: 2, src: '/assets/2cw_0018_GhieraGMT2.png' },
      { id: 3, src: '/assets/2cw_0019_GhieraGMT3.png' },
      { id: 4, src: '/assets/2cw_0020_GhieraGMT4.png' },
      { id: 5, src: '/assets/2cw_0021_GhieraGMT5.png' },
      { id: 6, src: '/assets/2cw_0022_GhieraGMT6.png' },
      { id: 7, src: '/assets/2cw_0023_GhieraGMT7.png' },
      { id: 8, src: '/assets/2cw_0024_GhieraGMT8.png' },
      { id: 9, src: '/assets/2cw_0025_GhieraGMT9.png' },
      { id: 10, src: '/assets/2cw_0026_GhieraGMT10.png' },
      { id: 11, src: '/assets/2cw_0027_GhieraGMT11.png' },
      { id: 12, src: '/assets/2cw_0028_GhieraGMT12.png' },
      { id: 13, src: '/assets/2cw_0029_GhieraGMT13.png' },
      { id: 14, src: '/assets/2cw_0030_GhieraGMT14.png' },
      { id: 15, src: '/assets/2cw_0031_GhieraGMT15.png' },
      { id: 16, src: '/assets/2cw_0032_GhieraGMT16.png' },
      { id: 17, src: '/assets/2cw_0033_GhieraGMT17.png' },
      { id: 18, src: '/assets/2cw_0034_GhieraGMT18.png' },
      { id: 19, src: '/assets/2cw_0035_GhieraGMT19.png' },
      { id: 20, src: '/assets/2cw_0036_GhieraGMT20.png' },
      { id: 21, src: '/assets/2cw_0037_GhieraGMT21.png' },
      { id: 22, src: '/assets/2cw_0038_GhieraGMT22.png' },
      { id: 23, src: '/assets/2cw_0039_GhieraGMT23.png' },
      { id: 24, src: '/assets/2cw_0040_GhieraGMT24.png' },
      { id: 25, src: '/assets/2cw_0041_GhieraGMT25.png' }
    ],
    bezel: [
      { id: 1, src: '/assets/2cw_0015_Quadrante3.png' },
      { id: 2, src: '/assets/2cw_0014_Quadrante2.png' },
      { id: 3, src: '/assets/2cw_0013_Quadrante1.png' },
    ],
    dial: [
      { id: 1, src: '/assets/2cw_0001_LancetteGMT1.png' },
      { id: 2, src: '/assets/2cw_0002_LancetteGMT2.png' },
      { id: 3, src: '/assets/2cw_0003_LancetteGMT3.png' },
      { id: 4, src: '/assets/2cw_0004_LancetteGMT4.png' },
      { id: 5, src: '/assets/2cw_0005_LancetteGMT5.png' },
      { id: 6, src: '/assets/2cw_0006_LancetteGMT6.png' },
      { id: 7, src: '/assets/2cw_0007_LancetteGMT7.png' },
      { id: 8, src: '/assets/2cw_0008_LancetteGMT8.png' },
      { id: 9, src: '/assets/2cw_0009_LancetteGMT9.png' }
],
    strap: [
      { id: 1, src: '/assets/2cw_0054_Cinturino1.png' },
      { id: 2, src: '/assets/2cw_0055_Cinturino2.png' },
      { id: 3, src: '/assets/2cw_0048_Cinturino3.png' },
      { id: 4, src: '/assets/2cw_0050_Cinturino4.png' },
      { id: 5, src: '/assets/2cw_0044_Cinturino5.png' },
      { id: 6, src: '/assets/2cw_0052_Cinturino6.png' },
      { id: 7, src: '/assets/2cw_0046_Cinturino7.png' },
      { id: 8, src: '/assets/2cw_0051_Cinturino8.png' },
      { id: 9, src: '/assets/2cw_0043_Cinturino9.png' },
      { id: 10, src: '/assets/2cw_0053_Cinturino10.png' },
      { id: 11, src: '/assets/2cw_0045_Cinturino11.png' },
      { id: 12, src: '/assets/2cw_0049_Cinturino12.png' },
      { id: 13, src: '/assets/2cw_0047_Cinturino13.png' },
      { id: 14, src: '/assets/2cw_0041_Cinturino14.png' },
      { id: 15, src: '/assets/2cw_0035_Cinturino15.png' },
      { id: 16, src: '/assets/2cw_0036_Cinturino16.png' },
      { id: 17, src: '/assets/2cw_0042_Cinturino17.png' },
      { id: 18, src: '/assets/2cw_0037_Cinturino18.png' },
      { id: 19, src: '/assets/2cw_0038_Cinturino19.png' }
    ],
    lancetta: [
      { id: 1, src: '/assets/2cw_0009_GMT1.png' },
      { id: 2, src: '/assets/2cw_0010_GMT2.png' },
      { id: 3, src: '/assets/2cw_0011_GMT3.png' },
      { id: 4, src: '/assets/2cw_0012_GMT4.png' },
      { id: 5, src: '/assets/2cw_0013_GMT5.png' },
      { id: 6, src: '/assets/2cw_0014_GMT6.png' },
      { id: 7, src: '/assets/2cw_0016_GMT7.png' },
      { id: 8, src: '/assets/2cw_0015_GMT8.png' },
      { id: 8, src: '/assets/2cw_0017_GMT10.png' }
    ]
  },
  boatking: {
    case: [
      { id: 1, src: '/assets/2cw_0034_Cassa1.png' },
      { id: 2, src: '/assets/2cw_0033_Cassa2.png' },
      { id: 3, src: '/assets/2cw_0032_Cassa3.png' },
      { id: 4, src: '/assets/2cw_0031_Cassa4.png' }
    ],
    ring: [
      { id: 1, src: '/assets/2cw_0001_GhieraBK1.png' },
      { id: 2, src: '/assets/2cw_0002_GhieraBK2.png' },
      { id: 3, src: '/assets/2cw_0003_GhieraBK3.png' },
      { id: 4, src: '/assets/2cw_0004_GhieraBK4.png' },
      { id: 5, src: '/assets/2cw_0005_GhieraBK5.png' },
      { id: 6, src: '/assets/2cw_0006_GhieraBK6.png' },
      { id: 7, src: '/assets/2cw_0007_GhieraBK7.png' },
      { id: 8, src: '/assets/2cw_0008_GhieraBK8.png' },
      { id: 9, src: '/assets/2cw_0009_GhieraBK9.png' },
      { id: 10, src: '/assets/2cw_0010_GhieraBK10.png' },
      { id: 11, src: '/assets/2cw_0011_GhieraBK11.png' },
      { id: 12, src: '/assets/2cw_0012_GhieraBK12.png' },
      { id: 13, src: '/assets/2cw_0013_GhieraBK13.png' },
      { id: 14, src: '/assets/2cw_0014_GhieraBK14.png' },
      { id: 15, src: '/assets/2cw_0015_GhieraBK15.png' }
    ],
    bezel: [
      { id: 1, src: '/assets/2cw_0015_Quadrante3.png' },
      { id: 2, src: '/assets/2cw_0014_Quadrante2.png' },
      { id: 3, src: '/assets/2cw_0013_Quadrante1.png' },
    ],
    dial: [
      { id: 1, src: '/assets/2cw_0009_Lancette1.png' },
      { id: 2, src: '/assets/2cw_0008_Lancette9.png' },
      { id: 3, src: '/assets/2cw_0007_Lancette8.png' },
      { id: 4, src: '/assets/2cw_0006_Lancette7.png' },
      { id: 5, src: '/assets/2cw_0005_Lancette6.png' },
      { id: 6, src: '/assets/2cw_0004_Lancette5.png' },
      { id: 7, src: '/assets/2cw_0003_Lancette4.png' },
      { id: 8, src: '/assets/2cw_0002_Lancette3.png' },
      { id: 9, src: '/assets/2cw_0001_Lancette10.png' },
      { id: 10, src: '/assets/2cw_0010_Lancette11.png' },
      { id: 11, src: '/assets/2cw_0011_Lancette12.png' },
      { id: 12, src: '/assets/2cw_0012_Lancette2.png' }
    ],
    strap: [
      { id: 1, src: '/assets/2cw_0054_Cinturino1.png' },
      { id: 2, src: '/assets/2cw_0055_Cinturino2.png' },
      { id: 3, src: '/assets/2cw_0048_Cinturino3.png' },
      { id: 4, src: '/assets/2cw_0050_Cinturino4.png' },
      { id: 5, src: '/assets/2cw_0044_Cinturino5.png' },
      { id: 6, src: '/assets/2cw_0052_Cinturino6.png' },
      { id: 7, src: '/assets/2cw_0046_Cinturino7.png' },
      { id: 8, src: '/assets/2cw_0051_Cinturino8.png' },
      { id: 9, src: '/assets/2cw_0043_Cinturino9.png' },
      { id: 10, src: '/assets/2cw_0053_Cinturino10.png' },
      { id: 11, src: '/assets/2cw_0045_Cinturino11.png' },
      { id: 12, src: '/assets/2cw_0049_Cinturino12.png' },
      { id: 13, src: '/assets/2cw_0047_Cinturino13.png' },
      { id: 14, src: '/assets/2cw_0041_Cinturino14.png' },
      { id: 15, src: '/assets/2cw_0035_Cinturino15.png' },
      { id: 16, src: '/assets/2cw_0036_Cinturino16.png' },
      { id: 17, src: '/assets/2cw_0042_Cinturino17.png' },
      { id: 18, src: '/assets/2cw_0037_Cinturino18.png' },
      { id: 19, src: '/assets/2cw_0038_Cinturino19.png' }
    ]
  }
});

const selectedModel = ref('seasub');

const levelMap = {
  seasub: [
    { key: "case", label: "Cassa" },
    { key: "bezel", label: "Quadrante" },
    { key: "ring", label: "Ghiera" },
    { key: "dial", label: "Lancette" },
    { key: "strap", label: "Cinturino" }
  ],
  jetlag: [
    { key: "case", label: "Cassa" },
    { key: "bezel", label: "Quadrante" },
    { key: "ring", label: "Ghiera" },
    { key: "dial", label: "Lancette" },
    { key: "lancetta", label: "Lancetta GMT" },
    { key: "strap", label: "Cinturino" }
  ],
  boatking: [
    { key: "case", label: "Cassa" },
    { key: "bezel", label: "Quadrante" },
    { key: "ring", label: "Ghiera" },
    { key: "dial", label: "Lancette" },
    { key: "strap", label: "Cinturino" }
  ]
};

const levels = computed(() => levelMap[selectedModel.value]);
const selectedLevel = ref(levels.value[0].key);

const configuration = ref({});

watch(selectedModel, () => {
  selectedLevel.value = levels.value[0].key;

  const modelConfig = configurations.value[selectedModel.value];
  const initial = {};
  for (const key in modelConfig) {
    initial[key] = modelConfig[key][0]?.id || null;
  }
  configuration.value = initial;

  document.title = `2CW Configurator - ${selectedModel.value.toUpperCase()}`;
});

const setLayer = (layer, direction) => {
  const items = configurations.value[selectedModel.value][layer];
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

const setModel = (model) => {
  selectedModel.value = model;
};

provide('settings', settings);
provide('configurations', configurations);
provide('configuration', configuration);
provide('selectedModel', selectedModel);
</script>

<template>
  <div class="container configurator d-flex flex-column align-items-center justify-content-center" 
     :class="{ 'debug': settings.debug }">
    <pre v-if="settings.debug">{{ configuration }}</pre>
    <img src="/assets/logo.svg" alt="Logo" class="logo" />
    <div class="model-selector">
      <button :class="{ active: selectedModel === 'seasub' }" @click="setModel('seasub')">SEASUB</button>
      <button :class="{ active: selectedModel === 'jetlag' }" @click="setModel('jetlag')">JETLAG</button>
      <button :class="{ active: selectedModel === 'boatking' }" @click="setModel('boatking')">BOAT KING</button>
    </div>
    <div class="layers" :style="{ width: settings.layerWidth + 'px', height: settings.layerHeight + 'px' }">
      <ConfiguratorLayer v-for="(layer, index) in levels" :key="index" :name="layer.key" />  
    </div>
    <nav class="navbar">
      <button v-for="(level, index) in levels" :key="index" @click="selectedLevel = level.key"
        :class="{ active: selectedLevel === level.key }">
        {{ level.label }}
      </button>
    </nav>
    <div class="controls">
      <button @click="setLayer(selectedLevel, -1)"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="ai ai-ArrowLeft"><path d="M11 5l-7 7 7 7"/><path d="M4 12h16"/></svg>
      </button>
      <button @click="setLayer(selectedLevel, 1)"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="ai ai-ArrowRight"><path d="M4 12h16"/><path d="M13 5l7 7-7 7"/></svg>
      </button>
    </div>
  </div>
</template>

<!-- Removed redundant data() block -->

<style lang="scss" scoped>

@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');

h1 {
  font-size: 2.7rem;
  font-weight: 600;
  font-family: "Inter", sans-serif;
  color: white;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 4rem;
  padding-right: 1.5rem;

  @media screen and (max-width: 768px) {
    font-size: 2.3rem;
    margin-bottom: 3.5rem;
    padding-right: 0rem;
  }

  @media screen and (max-width: 480px) {
    font-size: 2rem;
    margin-bottom: 3rem;
  }
}

.logo {
  width: 150px;
  margin-bottom: 20px;
  margin-top: 20px;
  padding-right: 1.5rem;
  opacity: .5;

  @media screen and (max-width: 768px) {
    width: 125px;
    padding-right: 0rem;
    margin-bottom: 10px;
  }

  @media screen and (max-width: 480px) {
    width: 100px;
  }
}

.configurator {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
  width: 100vw;
  padding: 20px 0;
  .layers {
    position: relative;
    overflow: hidden;
    margin-bottom: 4rem;
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
  
  @media screen and (max-width: 768px) {
  .layers {
    margin-bottom: 1rem;
  }
}


  .navbar {
    display: flex;
    justify-content: center;
    gap: 10px;
    flex-wrap: wrap;
    padding: 10px;
  }

  @media screen and (max-width: 768px) {
  .navbar {
    display: inline-flex;
    overflow-x: auto;
    overflow-y: hidden;
    flex-wrap: nowrap;
    white-space: nowrap;
    width: 100%;
    -webkit-overflow-scrolling: touch;
    scroll-behavior: smooth;
    padding-left: 9rem;
    gap: 4px;
  }

  body {
    overflow-x: auto;
  }

  .navbar::-webkit-scrollbar {
    display: none;
  }
}

.navbar button {
  background: none;
  border: none;
  box-shadow: none;
  padding: 0;
  font-size: 1.5rem;
  font-weight: 500;
  font-family: "Inter", serif;
  transition: all 0.3s ease-in-out;
  color: white;
  cursor: pointer;
  opacity: 0.5;
  padding: 1rem;

  @media screen and (max-width: 768px) {
    font-size: 1.4rem;
  }

  @media screen and (max-width: 480px) {
    font-size: 1.3rem;
  }
}
  .navbar button.active {
  opacity: 1;
  }
  .controls {
    display: flex;
    justify-content: center;
    gap: 10px;
    padding-right: 1rem;
    font-size: 0.9rem;
    min-width: 50px;

    @media screen and (max-width: 768px) {
    font-size: 0.9rem;
  }

     @media screen and (max-width: 480px) {
    margin-bottom: 4rem;
  }

  }
  .controls button {
    background: none;
  border: none;
  box-shadow: none;
  font-size: 1rem;
  transition: all 0.3s ease-in-out;
  color: white;
  cursor: pointer;
  padding: 1rem;
  width: 7px;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 40px;
  min-height: 40px;
  width: 6rem;

  @media screen and (max-width: 768px) {
    width: 5rem;
  }

  @media screen and (max-width: 480px) {
    width: 5rem;
  }
  }
}

.controls button svg {
  min-width: 40px;
  min-height: 40px;
}

  .model-selector {
    display: flex;
    gap: 1rem;
    margin-bottom: 2rem;
 
    button {
      background: none;
      color: white;
      padding: 0rem 1rem;
      font-size: 1.8rem;
      font-weight: 700;
      text-transform: uppercase;
      cursor: pointer;
      opacity: 0.5;
      transition: all 0.3s ease-in-out;
      border: none;
      box-shadow: none;
      outline: none;
      font-family: "Inter", sans-serif;
    }
 
    button.active {
      opacity: 1;
    }
  }


</style>
