<template>
    <header class="header">
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
  .header {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1000;
    width: 100%;
    height: 70px; 
    background-color: #f8f9fa; 
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .logo-link {
    display: inline-block;
    padding: 10px;
  }
  
  .logo {
    height: 80px; 
    width: auto;
  }
  </style>
  