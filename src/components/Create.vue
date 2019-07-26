<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h3>Dodaj agenta</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="addAgent">
          <div class="form-group">
            <label>Ime:</label>
            <input type="text" class="form-control" v-model="agent.name" />
          </div>
          <div class="form-group">
            <label>Lokacija:</label>
            <input type="text" class="form-control" v-model="agent.area" />
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Dodaj agenta" />
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {
    name: "DodajAgenta"
  },
  data() {
    return {
      agent: {}
    };
  },
  methods: {
    addAgent() {
      axios({
        url: "http://localhost:8080/agent",
        method: "post",
        auth: {
          username: "admin",
          password: "admin123"
        },
        data: {
          name: this.agent.name,
          area: this.agent.area
        }
      })
      .then(notify => {
          alert("Korisnik uspjesno dodan!")
          if(event){
              this.agent.name = "",
              this.agent.area =""
          }
      })
      .catch(error => {
        console.log(error);
      });
    }
  }
};
</script>