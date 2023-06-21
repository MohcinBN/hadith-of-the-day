<template>
<h1>The selected Hadith</h1>

<div>
    <div v-if="currentPost">
      <h2>{{ currentPost.title }}</h2>
      <p>{{ currentPost.body }}</p>
    </div>
    <div v-else>
      Loading...
    </div>
  </div>

</template>
<style>

</style>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      currentPost: null,
    };
  },
  mounted() {
    this.fetchPost();
  },
  methods: {
    fetchPost() {
      // Make an API request to get the current post
      // You can use axios or any other library for HTTP requests
      axios.get('http://localhost/hadith-api/index.php')
        .then(response => {
          this.currentPost = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>