<template>
    <div id="App">
      <h1>Population Data</h1>
      <ul>
        <li v-for="i in data" :key="i.ID">
          {{ i.country }}: {{ i.Population }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        data: []
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await fetch('https://datausa.io/api/data?drilldowns=Nation&measures=Population');
          const jsonData = await response.json();
          this.data = jsonData.data;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      }
    }
  };
  </script>