<template>
  <div>
    <h1>Hello</h1>
    <AddCitations
            @add-citations="addCitations"
    />
    <Blog
            v-if="citations.length"
            v-bind:citations="citations"
            @remove-text="removeText"
    />
    <p v-else>Пока новостей нет.</p>
  </div>
</template>

<script>
import Blog from '@/components/Blog'
import AddCitations from '@/components/AddCitations'
export default {
  name: 'app',
  data() {
    return {
      citations: [
        {id: 1, user: 'Kseniya', data: '19.01.2019', title: 'Добро пожаловать', completed: false},
        {id: 2, user: 'Artjom', data: '19.01.2019', title: 'Первый пост', completed: false}
      ]
    }
  },
  methods: {
    removeText(id) {
      this.citations = this.citations.filter(t => t.id !==id)
    },
    addCitations(citation) {
      this.citations.push(citation)
    },
    editMethod(citation) {
      this.citations = citation
    }
  },
  components: {
    Blog, AddCitations
  }
}
</script>

<style>

</style>
