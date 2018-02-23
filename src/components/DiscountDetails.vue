<template>
  <div class="details container">
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{discount.name}}
        <span class="pull-right">
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+discount.id">Edit</router-link>
            <button class="btn btn-danger" v-on:click="deleteDiscount(discount.id)">Delete</button>
            </span>
    </h1>
    <div class="well">


      <h4> View DiscountInfo Details</h4>



      <table class="table table-striped">
          <thead>
            <tr>

            </tr>
          </thead>
          <tbody>
            <tr >
             <td>Name</td>
              <td>{{discount.name}}</td>
            </tr>
            <tr >
           <td>Model</td>
              <td>{{discount.model}}</td>
            </tr>

            <tr >
             <td>description</td>
              <td>{{discount.description}}</td>
            </tr>
            <tr >
             <td>photo</td>
              <td>{{discount.photo}}</td>
            </tr>
            <tr >
             <td>discount</td>
              <td>{{discount.discount}}</td>
            </tr>
            <tr >
           <td>uploader</td>
              <td>{{discount.uploader}}</td>
            </tr>
          </tbody>
      </table>




    </div>

  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'discountdetails',
  data () {
    return {
      discount: ''

    }
  },
  methods:{

      fetchDiscount(idvalue){
          var self = this;
    //      this.$http.post('/Discount/findbyid.do' +/id)
      //axios.post('http://localhost:8080/api/discount',{id:idvalue})

      var params = new URLSearchParams();
      params.append('id', idvalue);

      axios.post('http://localhost:8080/api/discount', params)
.then(function(response){
      //      this.discount = response.body;

            self.discount =response.data.info ;

    //    console.log(discount);
    //        console.log(this.discount);
          })
          .catch(function (error) {
         console.log(error);
       })
 },
      deleteDiscount(idvalue){
          var self = this;
    //      this.$http.post('/Discount/deletediscountbyid.do'+id)
    var params = new URLSearchParams();
    params.append('id', idvalue);
    axios.post('http://localhost:8080/api/delete', params)
           .then(function(response){
            self.$router.push({path: '/', query: {alert: 'ID_'+idvalue+ ' Discount Deleted'}});
           })
          .catch(function (error) {
         console.log(error);
       });
  }
  },

  created: function(){
      this.fetchDiscount(this.$route.params.id);
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
