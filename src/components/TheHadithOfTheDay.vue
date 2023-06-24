<template>

<div>
    
    <div class="col-lg-8 mx-auto">
      <h1 class="text-end mb-5">الحديث المختار لليوم:</h1>
      <div v-if="currentPost" class="selected-hadith px-3">
        <!--The hadith body-->
        <p>{{ currentPost.body }}</p>
        <!--Toggle explanation-->
        <div>
          <button class="btn btn-secondary border-0" @click="togglexplanation">
            <span v-if="!showExplanation">إظهار شرح الحديث</span>
            <span v-else>إخفاء شرح الحديث</span>
          </button>
        </div>
        <!--The hadith explanation-->
        <p v-if="showExplanation && explanationIsExist" class="mt-3">
          <a :href="currentPost.explanation" target="_blank"> شرح الحديث</a>
        </p>
      </div>
      <div v-else>
        Loading...
      </div>
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
      showExplanation: false,
    };
  },
  mounted() {
    this.fetchPost();
  },
  methods: {
    fetchPost() {
      axios.get('http://hadithofday.com/api/index.php')
        .then(response => {
          this.currentPost = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    explanationIsExist() {
      this.currentPost.explanation.length > 0
    },
    togglexplanation() {
      this.showExplanation = !this.showExplanation;
    }
  },
};
</script>