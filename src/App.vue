<template>
  <div id="app" class="app-container">
    <!-- <header class="app-header">
      <h1>WizFit Challenge - Participating Schools</h1>
    </header> -->
    <SchoolList />
  </div>
</template>

<script>
import SchoolList from './components/SchoolList.vue';

export default {
  name: 'App',
  components: {
    SchoolList,
  },
};
</script>

<style scoped>
.app-container {
  text-align: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 20px;
}

.app-header {
  background-color: #673ab7; /* WizFit theme purple */
  padding: 20px;
  color: white;
  margin-bottom: 40px;
}

h1 {
  font-size: 2.5rem;
  margin: 0;
}

@media (max-width: 600px) {
  h1 {
    font-size: 2rem;
  }
}
</style>
