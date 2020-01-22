<template>
   <li>
      <span class="person">
         <strong>{{citation.user}} </strong>
         <strong>{{citation.data}}</strong>
      </span>
      <strong class="text">{{citation.title}}</strong>
      <span class="button">
         <button class="delete"
              v-on:click="$emit('remove-text', citation.id)"
         >Удалить</button>
         <button class="redactor"
                 v-on:click="$emit('transform-citation',citation)"
         >Редактировать</button>
      </span>
   </li>
</template>

<script>
export default {
   props: {
      citation: {
         type: Object,
         required: true
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