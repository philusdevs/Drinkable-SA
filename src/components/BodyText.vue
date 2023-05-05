<template>
    <div>
      <p v-if="!hideText">
        <strong>Disinfectants</strong> are used to kill microorganisms in water to ensure it is safe for human consumption, and 97% compliance with national standards refers to the percentage of water samples that meet the required level of disinfection.
      </p>
      <p v-if="!hideText">
        <strong>Non-health aesthetics</strong> refer to factors that affect the appearance, taste, and odor of water but do not pose a health risk, and 97% compliance with national standards refers to the percentage of water samples meeting aesthetic standards.
      </p>
      <p v-if="!hideText">
        <strong>Operational</strong> refers to the day-to-day activities involved in managing and maintaining water treatment and distribution systems, and 97% compliance refers to the percentage of operational tasks meeting required standards.
      </p>
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
  /* Your styles for the body text */
  </style>
  