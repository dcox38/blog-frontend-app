<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <hr>
    <h1> Title: {{ post.title }}</h1>
    <h1> Blog: {{ post.body }}</h1>

    <img v-bind:src="post.image">

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to the Show!",
      post: {}
    };
  },
  created: function() {
    this.showPost();

  },
  methods: {
    showPost: function() {
      console.log('show me the post!');
      console.log(this.$route);
      axios.get(`api/posts/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.post = response.data;
      });

    }
  }
};
</script>