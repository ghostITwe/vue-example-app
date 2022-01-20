<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
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
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
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
      axios.get('http://127.0.0.1:8000/posts')
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
