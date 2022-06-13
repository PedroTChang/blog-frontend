<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Index of Posts",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        console.log("posts index", response);
        this.posts = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="row">
      <div v-for="post in posts" v-bind:key="post.id">
        <h2>{{ post.title }}</h2>
        <img v-bind:src="post.image" v-bind:alt="post.title" />
        <div class="card-body">
          <router-link v-bind:to="`/posts/${post.id}`" class="btn btn-primary">More details</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
