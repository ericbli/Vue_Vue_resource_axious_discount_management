<template>
  <div class="edit container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Edit Discount</h1>
    <form v-on:submit="updateDiscount">
        <div class="well">


          <h4>DiscountInfo Details</h4>
          <div class="form-group">
              <label>Name</label>
              <input type="text" class="form-control" placeholder="Name" v-model="discount.name">
          </div>
          <div class="form-group">
              <label>Model</label>
              <input type="text" class="form-control" placeholder="Model" v-model="discount.model">
          </div>
          <div class="form-group">
              <label>description</label>
              <input type="text" class="form-control" placeholder="description" v-model="discount.description">
          </div>
          <div class="form-group">
              <label>photo</label>
              <input type="text" class="form-control" placeholder="photo" v-model="discount.photo">
          </div>
          <div class="form-group">
              <label>discount</label>
              <input type="text" class="form-control" placeholder="discount" v-model="discount.discount">
          </div>
          <div class="form-group">
              <label>uploader</label>
              <input type="text" class="form-control" placeholder="uploader" v-model="discount.uploader">
          </div>






        </div>

        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';
    import Alert from './Alert'
    export default {
    name: 'add',
    data () {
        return {
  //      discount: {},
            discount: '',
        alert:''
        }
    },
    methods: {
        fetchDiscount(idvalue){
              var self = this;
              var params = new URLSearchParams();
              params.append('id', idvalue);
        axios.post('http://localhost:8080/api/discount', params)
                .then(function(response){
            //      this.discount = response.body;
                self.discount =response.data.info ;

            //   console.log(discount);
          //        console.log(this.discount);
                })
                .catch(function (error) {
               console.log(error);
             })
        },
        updateDiscount(e){

            if(!this.discount.name || !this.discount.model || !this.discount.uploader){
                this.alert = 'Please fill in all required fields';
            } else {
                let updDiscount = {
                    name: this.discount.name,
                    model: this.discount.model,
                    description: this.discount.description,
                    uploader: this.discount.uploader,
                    discount: this.discount.discount,
                    photo: this.discount.photo,
                    id:this.discount.id
                }


                //axios.post('http://localhost:8080/api/update',{body:{updDiscount}} )

          //    axios.post('http://localhost:8080/api/update', updDiscount )
          //  .then(function(response){
          //    self.$router.push({path: '/', query: {alert:idvalue+ 'Discount Updated'}});


                        this.$http.post('http://localhost:8080/api/update', updDiscount)
                            .then(function(response){
                                this.$router.push({path: '/', query: {alert: 'Discount Info updated'}});




                    })
                    .catch(function (error) {
                   console.log(error);
                 });

                e.preventDefault();
            }
            e.preventDefault();
        }
    },
    created: function(){
        this.fetchDiscount(this.$route.params.id);
    },
    components:{
        Alert
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
