<template>

<div class="container">

    <div class="row justify-content-center my-5">
        <div class="col-6">
                                    <h2>Client List</h2>

            <div class="card mb-5">
                <div class="card-body">
                    
                    <div class="form-group mb-3">
                        
                        <input type="text" name="" id="" class="form-control" placeholder="Enter your Name" v-model="name">
                        </div>
                        <div class="form-group mb-3">
                            <textarea name="" id="" cols="30" rows="10" class="form-control" placeholder="Enter your City" v-model="city"></textarea>
                        </div>
                                                <div class="form-group mb-3">
                            <textarea name="" id="" cols="30" rows="10" class="form-control" placeholder="Enter your Address" v-model="address"></textarea>
                        </div>
                        <button class="btn btn-primary" v-on:click="addPost">ADD</button>
                    </div>
                </div>

            </div>
        </div>
                <div class="card mb-3" v-for="meets in meetups">
                    <div class="card-body">
                         <h3>{{meets.name}}</h3>
                        <p v-text="meets.city"></p>
                        <p v-text="meets.address"></p>
                        <!-- Use for testing -->
                         <!-- <p v-text="meets.id"></p> -->

                        </div>
                        <button class="btn btn-danger" v-on:click="deletePost(meets.id)">Delete</button>
                        
                        <!--Not Working <button class="btn btn-safe" v-on:click="updatePost(meets.id)">Edit</button> -->


                </div>
</div>

</template>



<script>
import axios from "axios";

export default {
  data() {
    return {
      message: "Hello world",
      meetups: [],
      name: "",
      city: "",
      address: "",
      id:""
    };
  },
  mounted() {
      this.getMeetups()
      console.log(this.meet)

  },
  methods: {
      addPost(){
          const data = {
              name: this.name,
              city: this.city,
              address: this.address
              }
          axios.post('http://localhost:3000/api/meetups', data).then(response =>{
              this.getMeetups()
              this.clearInput()
          })
      },
    getMeetups() {
      axios.get("http://localhost:3000/api/meetups/").then(response => {
        this.meetups = response.data;
        this.meetups.reverse()
      })
    },
    deletePost(id){
      axios.delete("http://localhost:3000/api/meetups/" + id).then(response => {
          this.getMeetups()
      })
    },
    // Working on update method
    //     updatePost(id){
    //   axios.put("http://localhost:3000/api/meetups/" + id ).then(response => {
    //       this.name = 
    //       this.city = 
    //       this.address =
    //       this.id = 
    //       this.getMeetups()
    //   })
    // },
    clearInput(){
        this.name = ''
        this.city = ''
    }
  }
};
</script>