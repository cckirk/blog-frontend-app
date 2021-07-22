<template>
  <div class="posts-edit">
    <form v-on="submit()">
      <h1>Edit Posts</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostsParams.title" />
      </div>
      <div>
        <label>Chef:</label>
        <input type="text" v-model="editPostsParams.chef" />
      </div>
      <div>
        <label>Ingredients:</label>
        <input type="text" v-model="editPostsParams.ingredients" />
      </div>
      <div>
        <label>Directions:</label>
        <input type="text" v-model="editPostsParams.directions" />
      </div>
      <div>
        <label>Prep Time:</label>
        <input type="text" v-model="editPostsParams.prep_time" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="editPostsParams.image_url" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editpostParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .patch(`/posts/${this.$route.params.id}`, this.editpostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts/" + this.$route.params.id);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    getpost: function () {
      console.log("getting post");
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.editpostParams = response.data;
      });
    },
  },
  created: function () {
    console.log("in created...");
    this.getpost();
  },
};
</script>