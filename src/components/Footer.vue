<template>
    <footer>
      <p>
        Data is taken from www.niwis.gov.za.</p>
      <p>All data is supplied free of charge and may not be sold to third parties.
      </p>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'AppFooter',
  };
  </script>
  
  <style>
footer {
  height: 20;
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
  