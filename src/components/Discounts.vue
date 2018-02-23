<template>
  <div class="discounts container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Manage Discounts</h1>
  <input class="form-control" placeholder="Enter Name" v-model="filterInput">
    <br />
    <table class="table table-striped">
        <thead>
          <tr>
            <th>Name</th>
            <th>Model</th>
            <th>Uploader</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <!--        <tr v-for="discount in discounts">-->
     <tr v-for="discount in filterBy(discounts, filterInput)">
            <td>{{discount.name}}</td>
            <td>{{discount.model}}</td>
            <td>{{discount.uploader}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/discount/'+discount.id">View</router-link></td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
  import Alert from './Alert';
  export default {
    name: 'discounts',
    data () {
      return {
        discounts: [],
        alert:'',
        filterInput:''
      }
    },
    methods: {
      fetchDiscounts(){

          this.$http.post('http://localhost:8080/api/discounts')
          .then(function(response){
            this.discounts =response.data.info ;

          });
      },
      filterBy(list, value){
        value = value.charAt(0).toUpperCase() + value.slice(1);
        return list.filter(function(discount){
          return discount.name.indexOf(value) > -1;
        });
      }
    },
    created: function(){
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert;
      }
      this.fetchDiscounts();
    },
 //updated: function(){
//this.fetchDiscounts();
// },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
