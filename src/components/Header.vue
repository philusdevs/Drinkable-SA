<template>
    <header>
      <a href="/" class="logo-link">
        <img :src="require('@/assets/logo.png')" alt="Website Logo" class="logo">
      </a>
    </header>
  </template>
  
  <script>
  export default {
    name: 'AppHeader',
  };
  </script>
  
  <style>
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

  </style>