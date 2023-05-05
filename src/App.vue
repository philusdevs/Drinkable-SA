<template>
  <div id="app">
    <header>
      <a href="index.html" class="logo-link">
      <img :src= "require('@/assets/logo.png')" alt="Website Logo" class="logo">
      </a>
    </header>
    <div class="content">
      <WaterQuality @selectionMade="hideInfoText" />
      <div v-if="!hideText">
        <p>
          <strong>Disinfectants</strong> are used to kill microorganisms in water to ensure it is safe for human consumption, and 97% compliance with national standards refers to the percentage of water samples that meet the required level of disinfection.
        </p>
        <p>
          <strong>Non-health aesthetics</strong> refer to factors that affect the appearance, taste, and odor of water but do not pose a health risk, and 97% compliance with national standards refers to the percentage of water samples meeting aesthetic standards.
        </p>
        <p>
          <strong>Operational</strong> refers to the day-to-day activities involved in managing and maintaining water treatment and distribution systems, and 97% compliance refers to the percentage of operational tasks meeting required standards.
        </p>
      </div>
    </div>
    <footer>
      <p >
        Data is taken from www.niwis.gov.za.The copyright of the data/information remains with the Department of Water and Sanitation. </p>
        <p>All data is supplied free of charge and may not be sold to third parties. The use of information data is restricted to use for academic, research, or personal purposes.
      </p>
    </footer>
  </div>
</template>

<script>
import WaterQuality from './components/WaterQuality.vue';

export default {
  name: 'App',
  components: {
    WaterQuality,
  },
};
</script>

<style>
/* Global styles */

header {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.logo-link {
  display: inline-block;
  padding: 10px;
}

.logo {
  height: 110px; 
  width: auto;
}

body {
  font-family: 'Arial', sans-serif;
  line-height: 1.6;
  color: #333;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.content {
  flex: 1;
}

h1, h2, h3 {
  margin-bottom: 1rem;
}

select {
  display: block;
  width: 100%;
  padding: 0.5rem;
  font-size: 1.2rem;
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

footer {
  height:20;
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  font-size: 0.4rem;
  text-align: center;
  padding: 1rem;
  background-color: #f8f9fa;
}

footer p {
  margin-bottom: 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>