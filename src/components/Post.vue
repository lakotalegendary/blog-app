<template lang="html">
  <div class="post" v-if="post">
    <h1 class="post__title">{{ post.title }}</h1>
    <p class="post__body">{{ post.body }}</p>
    <p class="post__id">{{ post.id }}</p>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    props: ['id'],
    data() {
      return {
        post: null,
        endpoint: 'https://jsonplaceholder.typicode.com/posts/',
      }
    },
    created() {
      this.getPost(this.id)
    },
    methods: {
      getPost(id) {
        axios.get(this.endpoint + id)
          .then(res => {
            this.post = res.data
          })
          .catch(err => {
            console.error(err);
          })
      }
    },
    watch: {
      '$route' () {
        this.getPost(this.id)
      }
    }
  }
</script>
