<script setup>

import { ref } from 'vue'

const showForm = ref(false)
const postHeader = ref('')
const postBody = ref('')
const postAuthor = ref('')
const posts = ref([])
const isMenuOpen = ref(false)
const loadPosts = localStorage.getItem('posts');
if(loadPosts){
  posts.value = JSON.parse(loadPosts);
} 




function submitForm()
{
  const newPost = {
    id: Date.now(),
    title: postHeader.value,
    body: postBody.value,
    author: postAuthor.value
  }
  posts.value.push(newPost)

  localStorage.setItem('posts', JSON.stringify(posts.value))


  showForm.value = false
  postHeader.value = ''
  postBody.value = ''
  postAuthor.value = ''
}

function deletePost(id)
{
  posts.value = posts.value.filter(post => post.id !== id);
  localStorage.setItem('posts', JSON.stringify(posts.value))
}

</script>

<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="class">📰 My Blog</div>
      <button class="menu-toggle" @click="isMenuOpen = !isMenuOpen">
        ☰
      </button>
      <ul :class="['nav-links', { open: isMenuOpen }]">
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/about">About</router-link></li>
      <li><button @click="showForm = true">New Post</button></li>
    </ul>
    </div>
  </nav>

  <h1>Blog Posts</h1>
  <div v-if="posts.length > 0" class="posts">
    <div v-for="post in posts" :key="post.id" class="post">
      <h3>{{ post.title }}</h3>
      <p>{{ post.body }}</p>
      <small>{{ post.author }}</small>
      <button @click="deletePost(post.id)">Delete Post</button>
    </div>
  </div>


  <form v-if="showForm" @submit.prevent="submitForm">
    <h1>Create Post</h1>
    <p>Post Header: <input type="text" required v-model="postHeader"></p>
    <p>Post Body: <input type="textarea" rows="4" cols="50" required v-model="postBody"></p>
    <p>Post Author: <input type="text" required v-model="postAuthor"></p>
    <button type="">Submit</button>
  </form>
</template>

<style scoped>

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 20px;
}

.navbar {
  background-color: #333;
  color: white;
  padding: 0.75rem 1rem;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.brand {
  font-size: 1.5rem;
  font-weight: bold;
}

.menu-toggle {
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
  display: none;
}

.nav-links {
  display: flex;
  gap: 1rem;
  list-style: none;
}

.nav-links li {
  margin: 0.5rem 0;
}

.nav-links a,
.nav-links button {
  color: white;
  text-decoration: none;
  background: none;
  border: none;
  cursor: pointer;
  font: inherit;
}

.nav-links button:hover,
.nav-links a:hover {
  text-decoration: underline;
}

form {
  margin: 2rem;
  padding: 2rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  max-width: 500px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

form h1 {
  margin-bottom: 1rem;
}

form p {
  margin-bottom: 1rem;
}

form input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}

form button {
  padding: 0.5rem 1.5rem;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

form button:hover {
  background-color: #218838;
}

.post {
  border: 1px solid #ddd;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 6px;
  background-color: #f9f9f9;
}

.posts {
  margin: 2rem;
  padding: 2rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  max-width: 500px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}


.post button {
  margin-top: 0.5rem;
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 0.4rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}

.post button:hover {
  background-color: #c82333;
}
</style>
