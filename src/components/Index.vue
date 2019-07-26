<template>
  <div>
    <h1>Agenti</h1>

    <table class="table table-hover">
      <thead>
        <tr>
          <td>Kod</td>
          <td>Ime</td>
          <td>Lokacija</td>
          <td>Akcije</td>
        </tr>
      </thead>

      <tbody>
        <tr v-for="agent in agents" :key="agent.code">
          <td>{{ agent.code }}</td>
          <td>{{ agent.name }}</td>
          <td>{{ agent.area }}</td>
          <td>
            <router-link :to="{name: 'Edit', params: { id: agent.code }}" class="btn btn-primary">Uredi</router-link>
          </td>
          <td>
            <button class="btn btn-danger" v-on:click="deleteAgent(agent.code)">Izbrisi</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      agents: []
    };
  },
  created: function() {
    this.fetachAll();
  },
  methods: {
    fetachAll() {
      axios({
        url: "http://localhost:8080/",
        method: "get",
        auth: {
          username: "admin",
          password: "admin123"
        }
      })
        .then(response => {
          this.agents = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    deleteAgent(code){
              axios({
        url: "http://localhost:8080/agent" + "/" + code,
        method: 'delete',
        auth: {
          username: "admin",
          password: "admin123"
        }
      })
        .then(refresh => {
        this.fetachAll();
           
        })
        .catch(error => {
          console.log(error);
        });
    }
    // ,
    // deleteItem(id) {
    //   let uri = "http://localhost:4000/items/delete/" + id;
    //   this.items.splice(id, 1);
    //   this.axios.get(uri);
    // }
  }
};
</script>