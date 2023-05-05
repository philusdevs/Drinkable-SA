<template>
    <div class="bodyText">
        <p v-if="!hideText"> The national standard of compliance is 97 % for Disinfectant, Non-health aesthetics and Operations.</p>

<p v-if="!hideText">
       <strong>Disinfectants</strong> refers to chemicals used to kill microorganisms in water to ensure it is safe for human consumption.
     </p>
     <p v-if="!hideText">
       <strong>Non-health aesthetics</strong> refer to factors that affect the appearance, taste, and odor of water but do not pose a health risk.
     </p>
     <p v-if="!hideText">
       <strong>Operations</strong> refers to the day-to-day activities involved at the Municipal.</p>
   </div>
  </template>
  
  <script>
  export default {
    name: 'BodyText',
    data() {
      return {
        hideText: false,
      };
    },
    methods: {
      hideInfoText() {
        this.hideText = true;
      },
    },
  };
  </script>
  
  <style>
  .bodyText{
 text-align: center;
  }
  </style>
  