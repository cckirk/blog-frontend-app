<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>id: {{ post.id }}</h1>
    <h1>body: {{ post.body }}</h1>
    <h1>image: {{ post.image }}</h1>
    <h1>img_url: {{ post.img_url }}</h1>
    <h1>title: {{ post.title }}</h1>
    <p><img v-bind:src="post.image_url"></p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>
  </div>
</template>

<style>
img {
  width: 200px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the show!",
      post: {},
    };
  },
  created: function () {
    this.postShow();
  },
  methods: {
    postShow: function () {
      console.log("getting a single post");
      console.log(this.$route);
      // get data from rails
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
