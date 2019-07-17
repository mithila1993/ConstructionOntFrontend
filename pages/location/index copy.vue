<template>
    <div>
        <div class="container">
        <h1>Locations</h1>

        
        
<form>
    <div class="row">
        <div class="col-md-4">
            <div class="form-group">
                   <select name="cars" class="form-control" v-model="locationValue" @change="locationSearch">
                     <option value="colombo">Colombo</option>
                        <option value="gampaha">Gampaha</option>
                        <option value="kaluthara">Kaluthara</option>
                    </select>
             </div>    
        </div>
    </div>
    {{list}}
</form>

    <div role="tablist" v-for="(item,index) in list" :key="item.id">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab" @click="clickAccordin(index,item.subject.substring(44))">
        <b-button block href="#" variant="info">{{ item.ide }}</b-button>
      </b-card-header>
      <b-collapse :visible="index === expanded" id="accordion-1" role="tabpanel">
        <b-card-body v-if="description != undefined">
                      <!-- <b-card-text>{{description}}</b-card-text> -->

          <b-card-text>{{description[0].address}} - {{description[0].city}} - {{description[0].phone}} - {{description[0].registrationNumber}} - {{description[0].type}} - {{description[0].started}} - {{description[0].email}} - {{description[0].object}}</b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>


        <!-- <ul>
            <li v-for="(item,index) in list" :key="item.id">
            {{index}} - {{ item.subject }} 
            </li>
        </ul> -->
        
        
    </div>
    </div>
    
</template>

<script>
import axios from "axios";
import Search from '../../components/Search';
export default {
    components:{
        Search
    },
    data(){
        return{
            list:[],
            locationValue:null,
            expanded:null,
            description:null

        }
    },
    methods:{
        locationSearch(){
            axios.get("http://localhost:8083/getLocationBasedServices?location="+ this.locationValue )
                .then(response => this.list = response.data)
        },
        clickAccordin(index,subject){
            this.expanded=index;
            console.log(subject);
            axios.get("http://localhost:8083/getProfile?name="+ subject )
                .then(response => this.description = response.data)
        }
    },
}
</script>

<style>

</style>
