<template>
  <div class="logout"></div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    console.log("in logout");
    delete axios.defaults.headers.common["Authorization"];
    localStorage.setItem("jwt");
    this.$router.push("/");
  },
};
</script>