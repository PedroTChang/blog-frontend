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
  methods: {
    destroyPost: function () {
      console.log("Destroying recipe...");
      axios.delete("/posts/" + this.post.id + ".json").then((response) => {
        console.log("posts destroy", response.data);
        this.$router.push("/posts");
      });
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    <div v-if="getUserId() == post.user_id">
      <p><router-link class="btn btn-primary" v-bind:to="`/posts/${post.id}/edit`">Edit Post</router-link></p>
      <p><button class="btn btn-primary" v-on:click="destroyPost()">Delete Post</button></p>
    </div>
    <router-link to="/posts/">Back to all posts</router-link>
  </div>
</template>

<style></style>
