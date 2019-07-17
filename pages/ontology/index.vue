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
      <form class="search-section">
        <div class="row">
          <div class="form-group col-md-12">
            <input
              type="locations"
              class="form-control"
              placeholder="Search Location"
              v-model="locationValue"
            />
          </div>
        </div>
        <div class="row">
          <div class="col-md-3">
            <div class="form-group">
              <label>Cost value</label>

              <select name="costs" class="form-control" v-model="costValue">
                <option
                  v-for="costLevel in costLevels"
                  :key="costLevel.id"
                  :value="costLevel.levels.substring(44)"
                >{{costLevel.levels.substring(44)}}</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label>Service</label>
              <div class="form-group col-md-12">
                <input type="locations" class="form-control" v-model="serviceValue" />
              </div>
            </div>
          </div>
        </div>
        <button @click.prevent="search" class="btn btn-primary">Search</button>
      </form>

      
        <div class="list-item row" v-for="item in list" :key="item.id">
          <div class="col-md-2">
              <img :src="item.image" alt="Italian Trulli" width="100px"/>
            </div> 
            <div class="col-md-10">
                    <nuxt-link :to="'/ontology/'+item.id.substring(44)">
                        <span class="list-title" >{{ item.name }}</span>
                    </nuxt-link>
                    
          <div>{{item.discription}}</div>
        
                </div> 
          
          </div>
      
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "../../components/Search";
export default {
  components: {
    Search
  },
  data() {
    return {
      list: [],
      searchValue: null,
      locationValue: null,
      costValue: null,
      serviceValue: "hotel",
      costLevels: null
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
        .get("http://localhost:8083/getCostLevels")
        .then(response => (this.costLevels = response.data));
      //const res = await axios.get("https://reqres.in/api/users");
      //const res = await axios.get("http://10.10.2.62:8083/classesList");
      //console.log(res.data);
      //this.list = res.data;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    search() {
      console.log(this.costValue);
      console.log(this.locationValue);
      console.log(this.serviceValue);

      axios
        .get(
          "http://localhost:8083/searchAdvance?location=" +
            this.locationValue +
            "&cost=" +
            this.costValue +
            "&service=" +
            this.serviceValue +
            ""
        )
        .then(response => (this.list = response.data));
    }
  },

  head() {
    return {
      title: "Services",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place"
        }
      ]
    };
  }
};
</script>

<style>
</style>
