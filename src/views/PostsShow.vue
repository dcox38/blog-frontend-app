<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <hr>
    <h1> Title: {{ post.title }}</h1>
    <h1> Blog: {{ post.body }}</h1>

    <img v-bind:src="post.image">

    <a v-bind:href="`/posts/${post.id}/edit`">Edit this post</a>

    <p><button v-on:click="deletePost()">Delete this Post</button></p>

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
      axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.post = response.data;
      });

    },

    deletePost: function() {
      console.log('deleting the post...');
      axios.delete(`/api/posts/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.$router.push('/posts');
      });
    }
  }
};
</script>