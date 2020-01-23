<template>
   <li>
      <span class="person">
         <strong>{{post.user.name}} </strong>
         <strong>{{new Date(post.date).toLocaleString()}}</strong>
      </span>
      <textarea rows="10" cols="195"
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
   li {
      border: 1px solid #ccc;
      padding: .5rem 1rem;
      margin-bottom: 1rem;
   }
   .person {
      display: flex;
      justify-content: space-between;
      padding: 10px 0 10px 0;
      margin: 0;
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
   .text {
      padding: 20px 0 20px 0;
   }

</style>