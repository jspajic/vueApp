<template>
  <div>
    <div>
      <button id="add">Dodaj agenta</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Kod</th>
          <th>Ime</th>
          <th>Lokacija</th>
          <th>Uredi</th>
          <th>Izbrisi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="agent.id" v-for="agent in agents">
          <td>{{agent.code}}</td>
          <td>{{agent.name}}</td>
          <td>{{agent.area}}</td>
          <td>
            <button>Uredi</button>
          </td>
          <td>
            <button v-on:click="deleteAgent(agent.code)">Izbrisi</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Agent from "./Agent";
import axios from "axios";
export default {
  name: "Agents",
  components: {
    Agent
  },
  props: ["agents"],
  methods: {
    deleteAgent(code) {
      axios({
        url: "http://localhost:8080/agent" + "/" + code,
        method: 'delete',
        auth: {
          username: "admin",
          password: "admin123"
        }
      })
        .then(refresh => {
        alert("Korisnik uspjesno izbrisan!")
           window.location.reload();
           
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
table {
  padding-left: 30%;
  border-radius: 3px;
  background-color: rgb(255, 255, 255);
}
th {
  background-color: #c0c0bb;
  color: rgb(255, 255, 255);
  min-width: 120px;
  padding: 10px 20px;
}
td {
  background-color: #f9f9f9;
  min-width: 120px;
  padding: 10px 20px;
}

#add {
  margin: 0% 40% 0% 38.3%;
  width: 20%;
}

button {
  background-color: #f9f9f9;
  padding: 10px 20px;
}
</style>