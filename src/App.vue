<template>
  <div>
    <h1 v-if="!currentUser">Добро пожаловать в SWEATER</h1>
    <div v-if="currentUser">
      <h2>Привет, {{currentUser.name}}. Мы тебе рады.</h2>
      <button class="out" v-on:click="logout">Выйти</button>
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
        {id: 2, name: 'Ксения', password: '2222'},
        {id: 3, name: 'Артём', password: '3333'},
        {id: 4, name: 'Александра', password: '4444'},
        {id: 5, name: 'Анастасия', password: '5555'},
        {id: 6, name: 'Василий', password: '6666'},
        {id: 7, name: 'Дед Мороз', password: '7777'},
        {id: 8, name: 'Кот', password: '8888'}
      ],
      posts: [
        {user: {id: 2, name: 'Ксения'}, date: 1579798392170, title: 'Добро пожаловать в SWEATER! :) Это как TWITTER только SWEATER'},
        {user: {id: 7, name: 'Дед Мороз'}, date: 1579795452151, title: 'Детки, идите в IТ. С НОВЫМ ГОДОМ!'},
        {user: {id: 5, name: 'Анастасия'}, date: 1579795464593, title: 'Вау, сегодня выпало столько снега, кто пойдёт лепить снеговика? ;)'},
        {user: {id: 6, name: 'Василий'}, date: 1579795475928, title: 'Ищу кота, выбежал когда я начал с ним делать кощачью гимнастиу. Помогите найти :('},
        {user: {id: 8, name: 'Кот'}, date: 1579795482571, title: 'Мяу :3'},
        {user: {id: 4, name: 'Александра'}, date: 1579795489083, title: 'Хочу выучить немецкий. Может я здесь такая не одна, если кто-то тоже хочет, напишите =)'},
        {user: {id: 3, name: 'Артём'}, date: 1579717918644, title: 'Кто хочет поехать на каток? Мне нужна компания :)'},
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
    Blog, AddPost, Authorise
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Dancing+Script');
  @import url('https://fonts.googleapis.com/css?family=Comfortaa:300,400,700&display=swap');
  body {
    overflow-x:hidden;
    margin: 0;
    padding: 0;
    background: url(https://cdn.pixabay.com/photo/2014/12/15/15/36/cloth-569222_960_720.jpg) no-repeat;
    background-attachment: fixed;
    background-size: cover;
  }
  h2 {
    margin: 15px 5px 10px 30px;
    text-align: left;
    color: cornflowerblue;
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
    margin: 15px;
  }
  .out {
    float: right;
    padding: 8px;
    margin: -60px 40px 30px 5px;
    font-weight: bold;
  }
</style>
