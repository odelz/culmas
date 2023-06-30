<script setup lang="ts">
import randomNum from './components/randomNum.vue';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';


</script>

<template>

  <main class="center-container">
    <div class="container">
      <randomNum/>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #F6F9FCff;
  height: 100vh; 
}

.container {
  background-color: #FFFFFF; /* White background for the container */
  border-radius: 10px; 
  padding: 20px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1); /* Box shadow */
  width: 400px; /* Fixed width for the container */
  height:400px;
}

/* Responsive styles */
@media (max-width: 600px) {
  .container {
    width: 90%; /* Adjust the width for smaller screens */
  }
}
</style>
