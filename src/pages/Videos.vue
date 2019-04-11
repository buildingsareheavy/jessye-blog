<template>
  <Layout :show-logo="true">
    <!-- Author intro -->
    <Author :show-title="true"/>

    <div class="videos">
      <div class="content-box">
        <p>Below are the vimeo videos.</p>
      </div>
    </div>
  </Layout>
</template>

<script>
import Author from "~/components/Author.vue";
import Axios from "axios";
import { log } from "util";
const axios = require("axios");

// How to See Authorization Header that set by Axios
// https://github.com/axios/axios/issues/1769
const getBaseUrl = () => {
  return "https://api.vimeo.com";
};

const axiosInstance = axios.create({
  baseURL: getBaseUrl(),
  timeout: 5000,
  headers: {
    Authorization: "Bearer 6334a2349097611dd0a16260b22d6f1b",
    "Content-Type": "application/json"
  }
});

export default {
  components: {
    Author
  },
  metaInfo: {
    title: "Videos"
  },
  data: function() {
    return {
      videos: []
    };
  },
  created() {
    // Make a request for a user with a given ID
    axiosInstance
      .get("/users/97249929/videos")
      .then(function(response) {
        // handle success
        console.log(response.data);
      })
      .catch(function(error) {
        // handle error
        console.log(error);
      })
      .then(function() {
        // always executed
      });
  }
};
</script>

<style lang="scss">
.videos {
}
</style>

