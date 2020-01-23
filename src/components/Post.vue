<template>
   <li>
      <span class="person">
         <strong>{{post.user.name}} </strong>
         <strong>{{new Date(post.date).toLocaleString()}}</strong>
      </span>
      <textarea rows="2" cols="98"
                v-on:change="changHandler"
                :disabled = "disabled"
      >{{post.title}}</textarea>
      <span class="button">
         <button class="delete"
              v-if="currentUser && currentUser.id === post.user.id"
              v-on:click="$emit('remove-text', post.date)"
         >Удалить</button>
         <button class="redactor"
                 v-if="currentUser && currentUser.id === post.user.id"
                 v-on:click="changDisabled"
         >Редактировать</button>
      </span>
   </li>
</template>

<script>
export default {
   data() {
      return {
         disabled: true
      }
   },
   props: {
      post: {
         type: Object,
         required: true
      },
      currentUser: {
         type: Object | null,
         required: true
      }
   },
   methods: {
      changHandler(event) {
         this.$emit('transform-post', this.post.date, event.target.value)
      },
      changDisabled() {
         this.disabled = !this.disabled
      }
   }
}
</script>

<style  scoped>
   @import url('https://fonts.googleapis.com/css?family=Arvo&display=swap');

   li {
      padding: .5rem 1rem;
      margin: 25px;
      color: white;
      font-family: 'Arvo', serif;
      font-size: 23px;
      border: 5px solid slategrey;
   }
   textarea {
      margin: 10px;
      resize: none;
      overflow: auto;
      background: transparent;
      border: none;
      font-size: 25px;
      color: white;
      font-family: 'Arvo', serif;
   }
   .person {
      display: flex;
      justify-content: space-between;
      padding: 10px 0 10px 0;

   }
   .button {
      display: flex;
      justify-content: flex-end;
   }
   .delete {
      font-weight: bold;
      background: pink;
   }
   .redactor {
      font-weight: bold;
      background: palegreen;
   }
</style>