<template>
  <Layout :show-logo="false">
    <!-- Author intro -->
    <Author :show-title="false"/>

    <div class="info">
      <div class="post-card content-box">
        <p>This is where your bio will go.</p>
        <p>Maybe a photo below, maybe not.</p>
      </div>
    </div>
  </Layout>
</template>

<script>
import Author from "~/components/Author.vue";

export default {
  components: {
    Author
  },
  metaInfo: {
    title: "Info"
  }
};
</script>

<style lang="scss">
</style>

