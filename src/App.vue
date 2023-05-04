<template>
  <div id="app">
    <WaterQuality />
    <footer>
      <p>
        The percentage shows the compliance with the national standards. A good indicator of compliance is 97 percentage and above.
      </p>
      <p>
        Data is taken from www.niwis.gov.za. The copyright of the data/information remains with the Department of Water and Sanitation. This approval to use the data/information cannot be construed as a transfer of copyright.
        All data is supplied free of charge and may not be sold to third parties. The use of information data is restricted to use for academic, research, or personal purposes.
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
body {
  font-family: 'Arial', sans-serif;
  line-height: 1.6;
  color: #333;
  margin: 0;
  padding: 0;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
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
  margin-top: 2rem;
  font-size: 0.9rem;
  text-align: justify;
}

footer p {
  margin-bottom: 1rem;
}
</style>

