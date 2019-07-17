<template>
    <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">Construction.lk</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" href="/ontology">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/Location">Location Based Services</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="title">
        <div class="container">
            <h1>Services</h1>
        </div>
    </div>
    
    <div class="container"> 
        <div class="profile" v-if="profile != undefined">
        <div class="row">
            <div class="col-md-3">
                    <img :src="profile[0].image" alt="Italian Trulli" width="200px"/>
            </div>
            <div class="col-md-9">
                <div class="profile-title">
                    {{profile[0].object}}
                </div>
                <div class="profile-address">
                    {{profile[0].address}}
                </div>
                <div class="profile-rest">
                    {{profile[0].city}}
                </div>
                <div class="profile-rest">
                    {{profile[0].phone}}
                </div>
                <div class="profile-rest">
                    {{profile[0].started}}
                </div>
                <div class="profile-rest">
                    {{profile[0].type}}
                </div>
                <div class="profile-rest">
                    {{profile[0].email}}
                </div>
                <a class="btn btn-danger profile-button text-light" @click="$router.go(-1)">back</a>
                
            </div>
        </div>
        </div>
    </div>
    </div>  
</template>

<script>
import axios from "axios";

export default {
    data() {
    return {
      profile: null,
    };
  },

  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      axios
        .get("http://localhost:8083/getProfile?name="+this.$route.params.id)
        .then(response => (this.profile = response.data));
      //const res = await axios.get("https://reqres.in/api/users");
      //const res = await axios.get("http://10.10.2.62:8083/classesList");
      //console.log(res.data);
      //this.list = res.data;
    } catch (err) {
      console.log(err);
    }
  },
}
</script>

<style>

</style>
