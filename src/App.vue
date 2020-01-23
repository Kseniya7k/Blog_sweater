<template>
  <div>
    <h1>Добро пожаловать в SWEATER</h1>
    <div v-if="currentUser">
      <h2>Hello, {{currentUser.name}}</h2>
      <button v-on:click="logout">Выйти</button>
    </div>
  <Authorise
          v-if="!currentUser"
          v-bind:currentUser="currentUser"
          @authorise="authorise"
          @registration="registration"
          class = "authorise"
  />
  <AddPost
          v-if="currentUser"
          @add-post="addPost"
  />
  <Blog
          v-if="posts.length"
          v-bind:posts="posts"
          v-bind:currentUser="currentUser"
          @remove-text="removeText"
          @transform-post="transformPost"
  />
  <p v-else>Пока новостей нет.</p>
  </div>
</template>

<script>
import Blog from '@/components/Blog'
import AddPost from '@/components/AddPost'
import Authorise from '@/components/Authorise'
export default {
  name: 'app',
  data() {
    return {
      currentUser: null,
      users: [
        {id: 1, name: '1', password: '1'},
        {id: 2, name: 'Kseniya', password: '2222'},
        {id: 3, name: 'Artyom', password: '3333'},
      ],
      posts: [
        {user: {id: 2, name: 'Kseniya'}, date: 1579717889281, title: 'Добро пожаловать'},
        {user: {id: 3, name: 'Artjom'}, date: 1579717918644, title: 'Первый пост'}
      ]
    }
  },
  methods: {
    removeText(date) {
      this.posts = this.posts.filter(t => t.date !== date)
    },
    authorise(login, password) {
      const user = this.users.find(u => u.name === login && u.password === password)
      if (user) {
        this.currentUser = user;
      }
    },
    registration(newUser) {
      this.users.push(newUser)
    },
    addPost(post) {
      post.user = {
        id: this.currentUser.id,
        name: this.currentUser.name
      };
      let newPosts = Array.from(this.posts);
      newPosts.push(post);
      this.posts = newPosts.sort((p1, p2) => new Date(p2.date) - new Date(p1.date))
    },
    transformPost(date, newValue) {
      this.posts.find(post => post.date === date).title = newValue;
    },
    logout() {
      this.currentUser = null
    }
  },
  components: {
    Blog, AddPost,Authorise
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Dancing+Script');
  @import url('https://fonts.googleapis.com/css?family=Comfortaa:300,400,700&display=swap');
  body {
    margin: 0;
    padding: 0;
    background: url(https://cdn.pixabay.com/photo/2014/12/15/15/36/cloth-569222_960_720.jpg) no-repeat;
    background-attachment: fixed;
    background-size: cover;
  }
  h2 {
    margin: 0;
    text-align: left;
    color: skyblue;
    text-shadow: black 0 0 1.5px;
    font-size: 50px;
    font-family: 'Dancing Script', cursive;
  }
  h1 {
    margin: 10px;
    text-align: center;
    color: cornflowerblue;
    text-shadow: black 0 0 1.5px;
    font-size: 50px;
    font-family: 'Dancing Script', cursive;
  }
  .authorise {
    text-align: center;
    margin: 20px;
  }
</style>
