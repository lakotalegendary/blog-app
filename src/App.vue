<template>
  <div id="app">
    <header>
      <h1>Vue.js Blog</h1>
    </header>
    <main class="blog-plate">
      <div></div>
      <aside class="sidebar">
        <ul>
          <li
            v-for="post in posts"
            :key="post.id">
            <router-link
              active-class="is-active"
              class="link"
              :to="{ name: 'post', params: { id: post.id } }">
              {{post.id}}. {{post.title}}
            </router-link>
            <br/>
          </li>
        </ul>
      </aside>
      <div class="content">
        <router-view></router-view>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: null,
      endpoint: 'https://jsonplaceholder.typicode.com/posts/',
    }
  },
  created() {
    this.getAllPosts();
  },
  methods: {
    getAllPosts() {
      axios.get(this.endpoint)
        .then(res => {
          this.posts = res.data;
        })
        .catch(err => {
          console.error('Error ' + err);
        });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding-left: 0;
  margin: 0;
  display: block;
}
li {
  margin: 0;
  float:left;
  text-align: left;
}
a {
  color: #42b983;
}
.blog-plate {
  display: grid;
  grid-template-columns: 1fr 3fr 6fr 1fr;
  grid-template-rows: 60px 9fr 1fr;
}
</style>
