<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id + ".json").then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="home">
    <h1>{{ post.title }}</h1>
    <!-- <img v-bind:src="post.image" v-bind:alt="post.image" /> -->
    <p>{{ post.body }}</p>
    <router-link to="/posts/">Back to all posts</router-link>
  </div>
</template>

<style></style>
