<template>
  <Layout :show-logo="false">
    <!-- Author intro -->
    <Author :show-title="true"/>

    <div class="video">
      <div class="post-card content-box" v-for="video in videos" :key="video.link">
        <p class="video-name">{{video.name}}</p>
        <p>{{video.description}}</p>
        <transition name="fade" appear>
          <div class="video-iframe">
            <iframe
              :src="'https://player.vimeo.com/video/' + video.link.slice(18) + '?title=0&byline=0&portrait=0'"
              frameborder="0"
              allow="autoplay; fullscreen"
              allowfullscreen
            ></iframe>
          </div>
        </transition>
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
    title: "Index"
  },
  props: {
    videos: Array
  },
  created() {
    // Make a request for a user with a given ID
    // https://developer.vimeo.com/api/reference/videos#get_videos
    axiosInstance
      .get("/users/97249929/videos")
      .then(response => {
        // handle success
        console.log(response.data);
        this.videos = response.data.data;
      })
      .catch(error => {
        // handle error
        console.log(error);
      });
  }
};
</script>

<style lang="scss">
.video {
  &-name {
    font-weight: 900;
    font-size: 1.5rem;
  }
  &-iframe {
    padding: 56.25% 0 0 0;
    position: relative;
    iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }
  }
}
</style>

