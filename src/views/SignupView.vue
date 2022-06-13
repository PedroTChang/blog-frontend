<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newUserParams.name" />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUserParams.password" />
        <p v-if="newUserParams.password && newUserParams.password.length > 20">
          <small class="text-danger">Cannot exceed 20 characters</small>
        </p>
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
        <p
          v-if="
            newUserParams.password_confirmation &&
            newUserParams.password &&
            newUserParams.password != newUserParams.password_confirmation
          "
        >
          <small class="text-danger">Passwords must match</small>
        </p>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
