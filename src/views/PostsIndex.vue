<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <h1>{{ greeting }}</h1>
    <hr>
    <h3>{{ posts }}</h3>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to the posts index!",
      greeting: "Here you will see some stuff",
      posts: []
    };
  },
  created: function() {
    this.indexPosts();

  },
  methods: {
    indexPosts: function () {
      console.log('posts index');
      axios.get('/api/posts').then(response => {
        console.log(response.data);
        this.posts = response.data;
      });
    } 
  }
};
</script>