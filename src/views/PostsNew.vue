<template>
  <div class="New-Post">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`">
    <form v-on:submit.prevent="submit()">
      <h1>Create a new post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label> 
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="body">
        <small v-if="body.length < 100">You have {{ 100 - body.length }} characters remaining</small>
        <small class="text-danger" v-if="body.length > 100">Your body must be under 100 characters</small>
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      body: "",
      image: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image,
      };

      console.log(params);

      axios
        .post("/api/posts", params)
        .then(response => {
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          console.log(error.response);
          this.status = error.response.status;
        });
    }
  }
};
</script>