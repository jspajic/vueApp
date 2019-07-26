<template>
  <div id="app">
    <Agents v-bind:agents="agents"/>
  </div>
</template>

<script>
import Agents from './components/Agents';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Agents
  },
  data(){
    return{
      agents: []
    }
  },
  created() {
    axios({
      url: 'http://localhost:8080',
      method: 'get',
      auth:{
        username:'admin',
        password:'admin123',
      }
    })
    .then(response => {
      this.agents = response.data;
      console.log("Auth!")
    })
    .catch(error => {
      console.log(error)
    })
  }
  }
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
