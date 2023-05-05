<template>
  <div id="app">
    <AppHeader />
    <div class="content">
      <WaterQuality @selectionMade="hideInfoText" />
      <BodyText ref="bodyText" />
    </div>
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/Header.vue';
import AppFooter from './components/Footer.vue';
import WaterQuality from './components/WaterQuality.vue';
import BodyText from './components/BodyText.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppFooter,
    WaterQuality,
    BodyText,
  },
  methods: {
    hideInfoText() {
      this.$refs.bodyText.hideInfoText();
    },
  },
};
</script>

<style>
/* Global styles */

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

</style>
