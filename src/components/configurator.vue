<script setup>
import { ref, onMounted, provide } from 'vue';
import ConfiguratorLayer from './configurator-layer.vue';

const backgroundColor = ref('#21002E');

onMounted(() => {
  document.body.style.backgroundColor = backgroundColor.value;

});

const settings = ref({
  layerWidth: 375,
  layerHeight: 450,
  debug: false,
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
     :class="{ 'debug': settings.debug }">
    <pre v-if="settings.debug">{{ configuration }}</pre>
    <img src="/assets/logo.svg" alt="Logo" class="logo" />
    <h1>SEASUB</h1>
    <div class="layers" :style="{ width: settings.layerWidth + 'px', height: settings.layerHeight + 'px' }">
      <img src="/assets/Glow.png" alt="Logo" class="glow" />
      <ConfiguratorLayer name="case" />    
      <ConfiguratorLayer name="bezel" />
      <ConfiguratorLayer name="ring" />  
      <ConfiguratorLayer name="dial" />
    </div>
    <nav class="navbar">
      <button v-for="(level, index) in levels" :key="index" @click="selectedLevel = level"
        :class="{ active: selectedLevel === level }">
        {{ ['Cassa', 'Quadrante', 'Ghiera', 'Lancette'][index] }}
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

.glow {
  object-position: center;
  position: absolute;
  top: 0;
  left: 0;
  width: 450px;
  height: 450px;
  object-fit: cover;
  z-index: 0;
  padding-right: 4rem;
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

.glow {
    height: 100%;
    width: auto;
    max-width: 100%;
    object-fit: cover;
  }

@media screen and (min-width: 768px) {
  .glow {
    height: 100%;
    width: auto;
    max-width: 100%;
    object-fit: cover;
    padding-left: 7rem;
  }
}
</style>
