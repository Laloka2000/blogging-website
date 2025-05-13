<script setup>
import { ref } from 'vue'

const showForm = ref(false)

const postHeader = ref('')
const postBody = ref('')
const postAuthor = ref('')

const posts = ref([])


function submitForm()
{
 const newPost = {
   title: postHeader.value,
   body: postBody.value, 
   author: postAuthor.value
 }

 posts.value.push(newPost)





  console.log('Submitted:', {
    title: postHeader.value,
    body: postBody.value,
    author: postAuthor.value,
  })

  showForm.value = false
  postHeader.value = ''
  postBody.value = ''
  postAuthor.value = ''
}

function deletePost(id){
  posts.value = posts.value.filter(post => post.id !== id);
}

</script>

<template>

  <menu>
    <li>
      <router-link to="/">Home</router-link>
    </li>
    <li>
      <router-link to="/about">About</router-link>
    </li>
    <div>
      <button @click="showForm = true">
        New Post
      </button>
    </div>
  </menu> 

  <div v-if="posts.length > 0" class="posts">
    <h2>Blog</h2>
    <div v-for="post in posts" :key="post.id" class="post">
      <h3>{{ post.title }}</h3>
      <p>{{ post.body }}</p>
      <small>{{ post.author}}</small>
      <button @click="deletePost(post.id)">Delete Post</button>
    </div>
  </div>


  <form v-if="showForm" @submit.prevent="submitForm">
    <h1>Create Post</h1>
    <p>Post Header: <input type="text" required v-model="postHeader"></p>
    <p>Post Body: <input type="textbox" required v-model="postBody"></p>
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

menu {
  display: flex;
  gap: 1rem;
  background-color: #f5f5f5;
  padding: 1rem;
  list-style: none;
  align-items: center;
  border-bottom: 1px solid #ccc;  
}

menu li {
  margin: 0;
}

menu a{
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

menu a:hover{
  color: #007BFF;
}

menu button {
  padding: 0.5rem 1rem;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

menu button:hover {
  background-color: #0056b3;
}

form{
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

.posts{
  margin: 2rem;
  padding: 2rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  max-width: 500px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}


.post button{
  margin-top: 0.5rem;
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 0.4rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}

.post button:hover{
  background-color: #c82333;
}

</style>
