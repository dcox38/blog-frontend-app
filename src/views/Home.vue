<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <p>{{ message }}</p>
    <hr>
    <h6>{{ message }}</h6>
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      message: "Congratulations!"
    };
  },
  created: function() {},
  methods: {}
};
</script>