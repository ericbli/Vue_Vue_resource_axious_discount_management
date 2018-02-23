<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Add DiscountInfo</h1>
    <form v-on:submit="addDiscount">
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
    import Alert from './Alert'
    export default {
    name: 'add',
    data () {
        return {
        discount: {},
        alert:''
        }
    },
    methods: {
        addDiscount(e){
            if(!this.discount.name || !this.discount.model || !this.discount.uploader){
                this.alert = 'Please fill in all required fields';
            } else {
                let newDiscount = {
                    name: this.discount.name,
                    model: this.discount.model,
                    description: this.discount.description,
                    uploader: this.discount.uploader,
                    discount: this.discount.discount,
                    photo: this.discount.photo,

                }

                this.$http.post('http://localhost:8080/api/add', newDiscount)
                    .then(function(response){
                        this.$router.push({path: '/', query: {alert: 'Discount Info Added'}});
                    });

                e.preventDefault();
            }
            e.preventDefault();
        }
    },
    components: {
        Alert
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
