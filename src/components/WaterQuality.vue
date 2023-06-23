<template>
  <div>
    <h1>Water Quality Checker</h1>
    <select v-model="selectedMunicipal" @change="calculateWaterSafety">
      <option value="">Select a Municipal to Check Water Quality</option>
      <option v-for="municipal in municipals" :key="municipal">{{ municipal }}</option>
    </select>

    <div v-if="selectedMunicipal">
      <h2>Water Quality for {{ selectedMunicipal }}</h2>
      <div>
        <h3>Disinfectant</h3>
        <p :style="{ color: getSafetyColor('disinfectant') }">{{ disinfectantSafety }} {{ selectedMunicipalData.disinfectant }}</p>
      </div>
      <div>
        <h3>Non-Health Aesthetic</h3>
        <p :style="{ color: getSafetyColor('nonHealthAesthetic') }">{{ nonHealthAestheticSafety }} {{ selectedMunicipalData.non_health_aesthetic }}</p>
      </div>
      <div>
        <h3>Operations</h3>
        <p :style="{ color: getSafetyColor('operational') }">{{ operationalSafety }} {{ selectedMunicipalData.operational }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'WaterQuality',

  data() {
    return {
      municipals: [],                 // Array to store the list of municipalities
      selectedMunicipal: '',          // Currently selected municipal
      waterQualityData: [],           // Array to store water quality data
      disinfectantSafety: '',         // Safety status for disinfectant
      nonHealthAestheticSafety: '',   // Safety status for non-health aesthetic
      operationalSafety: '',          // Safety status for operational
      selectedMunicipalData: {},      // Data of the selected municipal
    };
  },

  methods: {
    async fetchData() {
      try {
        // Fetch the list of municipalities and water quality data from the API
        const response = await axios.get('https://drinkablesa-api-b93993490e91.herokuapp.com/municipalities');
        this.waterQualityData = response.data.municipalities;
        this.municipals = this.waterQualityData.map((item) => item.name);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },

    async calculateWaterSafety() {
      try {
        // Fetch the specific data for the selected municipal from the API
        const response = await axios.get(`https://drinkablesa-api-b93993490e91.herokuapp.com/municipalities/${this.selectedMunicipal}`);
        this.selectedMunicipalData = response.data;

        // Calculate safety status based on the fetched data
        this.disinfectantSafety = this.selectedMunicipalData.disinfectant === "No Data" ? '' :
          parseFloat(this.selectedMunicipalData.disinfectant) < 97 ? 'Please boil water before drinking. Current compliance is at' : 'Drinkable';

        this.nonHealthAestheticSafety = this.selectedMunicipalData.non_health_aesthetic === "No Data" ? 'No Data Available' :
          parseFloat(this.selectedMunicipalData.non_health_aesthetic) < 97 ? 'Water may be affected in appearance, taste, and odor, but does not pose a health risk. Current compliance is at' : 'Drinkable';

        this.operationalSafety = this.selectedMunicipalData.operational === "No Data" ? 'No Data Available' :
          parseFloat(this.selectedMunicipalData.operational) >= 97 ? 'Good' : 'Municipal is not meeting the operations compliance standard of 97%. Current municipal compliance is at';
      } catch (error) {
        console.error('Error fetching municipal data:', error);
      }
    },

    getSafetyColor(safetyCategory) {
      // Get the safety status based on the safety category
      let safetyStatus = '';

      switch (safetyCategory) {
        case 'disinfectant':
          safetyStatus = this.disinfectantSafety;
          break;
        case 'nonHealthAesthetic':
          safetyStatus = this.nonHealthAestheticSafety;
          break;
        case 'operational':
          safetyStatus = this.operationalSafety;
          break;
      }

      if (safetyStatus === '') {
        return 'gray';
      }

      return safetyStatus === 'Good' || safetyStatus === 'Drinkable' ? 'green' : 'red';
    },
  },

  mounted() {
    this.fetchData();
  },
};
</script>

<style>
h1, h2, h3 {
  margin-bottom: 2rem;
}

h1 {
  text-align: center;
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
</style>
