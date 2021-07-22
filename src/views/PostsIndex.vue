<template>
  <div class="home">
    <!-- <h1>{{ posts }}</h1> -->
    <div v-for="post in posts" v-bind:key="post.id">
      <p>{{ post.id }}</p>
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <p>{{ post.image }}</p>
      <p><img v-bind:src="post.image_url"></p>
      <hr>
      <a v-bind:href="`posts/${post.id}`">1</a>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the index page!",
      posts: [],
    };
  },
  created: function () {
    this.PostsIndex();
  },
  methods: {
    PostsIndex: function () {
      console.log("in index posts");
      axios.get("/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>