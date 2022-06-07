<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      console.log("posts show", response);
      this.post = response.data;
      this.editPostParams = this.post;
    });
  },
  methods: {
    updatePost: function (post) {
      axios
        .patch("/posts/" + post.id, this.editPostParams)
        .then((response) => {
          console.log("posts update", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("posts update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-edit">
    <h1>Edit Post</h1>
    <form v-on:submit.prevent="updatePost(post)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Content:</label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="editPostParams.image" />
      </div>
      <input type="submit" value="Update" />
    </form>
  </div>
</template>
