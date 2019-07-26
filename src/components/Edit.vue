<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h3>Uredi Agenta</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="updateAgent">
          <div class="form-group">
            <label>Ime:</label>
            <input type="text" class="form-control" v-model="agent.name" />
          </div>
          <div class="form-group">
            <label>Lokacija:</label>
            <input type="text" class="form-control" v-model="agent.area" />
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Azuriraj podatke" />
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      agent: {}
    };
  },
  created: function() {
    this.getAgent();
  },
  methods: {
    getAgent() {
      axios({
        url: "http://localhost:8080/agent/" + this.$route.params.id,
        method: "get",
        auth: {
          username: "admin",
          password: "admin123"
        }
      })
        .then(response => {
          this.agent = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    updateAgent() {
      axios({
        url: "http://localhost:8080/agent/" + this.$route.params.id,
        method: "put",
        auth: {
          username: "admin",
          password: "admin123"
        },
        data: {

          name: this.agent.name,
          area: this.agent.area
        }
      })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>