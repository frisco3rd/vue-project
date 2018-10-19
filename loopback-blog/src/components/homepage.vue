<template>

<div class="container">
    <div class="row justify-content-center my-5">
        <div class="col-6">
            <div class="card mb-5">
                <div class="card-body">
                    <div class="form-group mb-3">
                        <input type="text" name="" id="" class="form-control" placeholder="Enter Title" v-model="name">
                        </div>
                        <div class="form-group mb-3">
                            <textarea name="" id="" cols="30" rows="10" class="form-control" placeholder="Enter your content" v-model="city"></textarea>
                        </div>
                        <button class="btn btn-primary" v-on:click="addPost">ADD</button>
                    </div>
                </div>

            </div>
        </div>
                    <h2> Post List </h2>
                <div class="card mb-3" v-for="meets in meetups">
                    <div class="card-body">
                         <h3>{{meets.name}}</h3>
                        <p v-text="meets.city"></p>
                        <p v-text="meets.address"></p>
                        </div>
                <button class="btn btn-danger" v-on:click="deletePost">Delete</button>


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
      id:""
    };
  },
  mounted() {
      this.getMeetups()
  },
  methods: {
      addPost(){
          const data = {
              name: this.name,
              city: this.city,
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
          this.meetups.splice(id,1)
        console.log(response)
      })
    },
    clearInput(){
        this.name = ''
        this.city = ''
    }
  }
};
</script>