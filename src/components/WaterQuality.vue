<template>
    <div>
      <h1>Drinkable-SA: Water Quality Checker</h1>
      <select v-model="selectedMunicipal" @change="calculateWaterSafety">
        <option value="">Select a Municipal</option>
        <option v-for="municipal in municipals" :key="municipal">{{ municipal }}</option>
      </select>
  
      <div v-if="selectedMunicipal">
        <h2>Water Quality Information for {{ selectedMunicipal }}</h2>
        <div>
          <h3>Disinfectant</h3>
          <p :style="{ color: getSafetyColor('disinfectant') }">{{ disinfectantSafety }} ({{ selectedMunicipalData.disinfectant }})</p>
        </div>
        <div>
          <h3>Non-Health Aesthetic</h3>
          <p :style="{ color: getSafetyColor('nonHealthAesthetic') }">{{ nonHealthAestheticSafety }} ({{ selectedMunicipalData.non_health_aesthetic }})</p>
        </div>
        <div>
          <h3>Operational</h3>
          <p :style="{ color: getSafetyColor('operational') }">{{ operationalSafety }} ({{ selectedMunicipalData.operational }})</p>
        </div>
      </div>
    </div>
</template>

  
  <script>
  import axios from 'axios';
  import Papa from 'papaparse';
  
  export default {
    name: 'WaterQuality',
    //settting up data() function,with the required data properties
    data() {
      return {
        municipals: [],
        selectedMunicipal: '',
        waterQualityData: [],
        disinfectantSafety: '',
        nonHealthAestheticSafety: '',
        operationalSafety: '',
        selectedMunicipalData: {},
      };
    },
    methods: {
        //Adds an object, to fetch the data from the GitHub CSV file and parse it:
      async fetchData() {
        const response = await axios.get('https://raw.githubusercontent.com/philusdevs/Drinkable-SA/main/Drinkable.csv');
        const csvData = response.data;
  
        Papa.parse(csvData, {
          header: true,
          complete: (results) => {
            this.waterQualityData = results.data.map((item) => {
              return {
                municipal: item.Municipal,
                disinfectant: item.Disinfectant,
                non_health_aesthetic: item['Non Health Aesthetic'],
                operational: item.Operational,
              };
            });
            this.municipals = Array.from(new Set(this.waterQualityData.map((item) => item.municipal)));
          },
        });
      },
  //// Measures the water safety based on the compliance percentage of each Municipal

      calculateWaterSafety() {
        const municipalData = this.waterQualityData.find(
          (item) => item.municipal === this.selectedMunicipal
        );

        this.selectedMunicipalData = municipalData;
  
        this.disinfectantSafety = municipalData.disinfectant === "No Data" ? 'No Data Available' :
          parseFloat(municipalData.disinfectant) < 97 ? 'Not Safe, Please Boil Water Before Drinking' : 'Drinkable';
  
        this.nonHealthAestheticSafety = municipalData.non_health_aesthetic === "No Data" ? 'No Data Available' :
          parseFloat(municipalData.non_health_aesthetic) < 97 ? 'Water maybe affected in appearance, taste, and odor of water, but does not pose a health risk. For example, water with a musty or earthy odor may be unpalatable, but it may not necessarily be harmful to drink.' : 'Drinkable';
  
        this.operationalSafety = municipalData.operational === "No Data" ? 'No Data Available' :
          parseFloat(municipalData.operational) >= 97 ? 'Good' : 'Not Good, Municipal is not meeting the compliance standard.';
      },
  
getSafetyColor(safetyCategory) {
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

  if (safetyStatus === 'No Data Available') {
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