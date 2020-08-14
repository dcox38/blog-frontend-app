<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <input type="text" v-model="search" list="titles">
    <hr>

    <datalist id="titles">
      <option v-for="post in posts">{{ post.title }}</option>
    </datalist>



    <hr>
    <div v-for="post in filterBy(posts, search, 'title')">
      <h3><a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></h3>
      <p>{{ post.body }}</p>
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import Vue2Filters from 'vue2-filters';

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to the posts index!",
      greeting: "Here you will see some stuff",
      posts: [],
      search: ""
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