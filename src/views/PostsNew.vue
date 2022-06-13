<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
      errorStatus: null,
    };
  },
  created: function () {},
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostParams)
        .then((response) => {
          console.log("posts create", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.errorStatus = error.response.status;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <img v-if="errorStatus" v-bind:src="`https://http.cat/${errorStatus}`" />
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Content:</label>
        <input type="text" v-model="newPostParams.body" />
        <small>
          <p v-if="newPostParams.body">Character Count : {{ newPostParams.body.length }}</p>
        </small>
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Create" />
    </form>
  </div>
</template>
