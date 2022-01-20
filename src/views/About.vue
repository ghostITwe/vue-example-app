<template>
  <div class="about">
    <div>
      <ul v-if="posts && posts.length">
        <li v-for="(index, post) of posts" :key="index">
          <p>{{ post.title }}</p>
          <p>{{ post.text }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'About',
  data() {
    return {
      posts: [],
      errors: []
    }
  },
  created() {
    this.getAllPosts();
  },
  methods: {
    getAllPosts() {
      axios.get('/sanctum/csrf-cookie').then(response => {
        console.log(response.data)
      });
      axios.get('http://127.0.0.1:8000/posts', {
        headers: {
          'Access-Control-Allow-Origin': 1
        }
      })
          .then(response => {
            this.posts = response.data
          })
          .catch(e => {
            this.errors.push(e)
          });
    }
  }
}
</script>
