<script setup>
import { computed, defineProps, inject } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true
  }
});

const settings = inject("settings");
const configurations = inject("configurations");
const configuration = inject("configuration");

const selectedModel = inject("selectedModel");

const images = computed(() => {
  return configurations.value[selectedModel.value]?.[props.name] || [];
});

const selectedIndex = computed(() => {
  return images.value.findIndex(item => item.id === configuration.value[props.name]);
});


</script>

<template>
  <div class="layer-container">
    <div 
      class="layer"
      v-for="(image, index) in images" 
      :key="image.id"
      :class="{ active: index === selectedIndex, prev: index < selectedIndex, next: index > selectedIndex }"
    >
      <img 
        :src="image.src" 
        alt="Layer Image" 
        class="configurator-image"
      />
    </div>
  </div>
</template>

<style scoped>
.layer-container {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.layer {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  transition: transform 0.5s ease-in-out, opacity 0.5s ease-in-out;
  opacity: 1; 
}

.layer.active {
  transform: translateX(0);
  opacity: 1;
  z-index: 3;
}

.layer.prev {
  transform: translateX(-100%);
  opacity: 1;
  z-index: 2;
}

.layer.next {
  transform: translateX(100%);
  opacity: 1;
  z-index: 2;
}

.configurator-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
